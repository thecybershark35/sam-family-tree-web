# Comprehensive Cursor Prompt for SamFamilyTreeWeb

This prompt will guide Cursor to start implementing the core functionality of our interactive Family Tree web application, focusing on the primary interactive tree visualization component.

Build a modern, responsive family history web application with React and TypeScript. This application will feature an intuitive, interactive family tree visualization with detailed person profiles, geographical mapping of family migration patterns, and intelligent data organization.

## Step 1: Project Setup

Initialize a new React project with TypeScript:
- Use create-react-app with TypeScript template
- Configure ESLint and Prettier for code quality
- Set up the basic folder structure for components, services, and utilities
- Install necessary dependencies:
  - d3 (v7+) for tree visualization
  - leaflet for map display
  - material-ui for UI components
  - styled-components for styling
  - react-router-dom for navigation

## Step 2: Create the Core Family Tree Component

Create a `FamilyTree` component at src/components/FamilyTree/FamilyTree.tsx with:

1. An interactive D3.js-powered tree visualization that:
   - Initially shows a mostly collapsed view with only root and immediate family
   - Allows clicking on nodes to expand/collapse them, making the clicked node the new focus
   - Supports click-and-drag to move the tree within the viewport
   - Enables mouse-wheel zoom with smooth transitions
   - Includes "Expand All" and "Collapse All" buttons with automatic spacing adjustment
   - Creates an SVG export function for large trees
   
2. Each node in the tree should display:
   - Person's full name prominently
   - Circular headshot image (with placeholder if none provided)
   - Age (calculated from birth/death dates)
   - Alive/deceased indicator (green/red dot)
   - Birth/death dates and places (abbreviated)
   - Generation indicator relative to root (e.g., "Gen 2")
   - Relationship streams (lines showing connections between related nodes)
   
3. Support for both small and large family trees:
   - Implement virtualization techniques for trees with 100+ members
   - Use Level of Detail (LOD) to simplify distant nodes when zoomed out
   - Implement lazy loading of expanded branches

## Step 3: Implement the Person Data Model

Create a TypeScript interface for person data at src/types/Person.ts:

```typescript
interface Location {
  place: string;
  latitude?: number;
  longitude?: number;
}

interface Person {
  id: string;
  name: string;
  image?: string;
  birthDate: string | null;
  birthPlace: Location | null;
  deathDate: string | null;
  deathPlace: Location | null;
  isAlive: boolean;
  gender: 'male' | 'female' | 'other' | 'unknown';
  generation: number;
  relationships: {
    parents: string[];
    children: string[];
    spouses: Array<{
      id: string;
      startDate?: string;
      endDate?: string;
      current: boolean;
    }>;
    siblings: string[];
  };
  events: Array<{
    type: string;
    date: string;
    location?: Location;
    description?: string;
  }>;
  children: Person[];
}
```

## Step 4: Create Sample Data

For development, start with this sample family data structure:

```javascript
const sampleFamilyData = {
  id: "1",
  name: "John Doe",
  image: "/placeholders/john.jpg",
  birthDate: "1950-01-01",
  birthPlace: { place: "New York, USA", latitude: 40.7128, longitude: -74.0060 },
  deathDate: null,
  deathPlace: null,
  isAlive: true,
  gender: "male",
  generation: 1,
  relationships: {
    parents: [],
    children: ["2", "3"],
    spouses: [{ id: "4", startDate: "1972-06-15", endDate: null, current: true }],
    siblings: []
  },
  events: [
    { type: "birth", date: "1950-01-01", location: { place: "New York, USA" } },
    { type: "graduation", date: "1972-05-30", location: { place: "Boston, USA" } },
    { type: "marriage", date: "1972-06-15", location: { place: "Boston, USA" } }
  ],
  children: [
    {
      id: "2",
      name: "Jane Doe",
      image: "/placeholders/jane.jpg",
      birthDate: "1975-05-05",
      birthPlace: { place: "Los Angeles, USA", latitude: 34.0522, longitude: -118.2437 },
      deathDate: null,
      deathPlace: null,
      isAlive: true,
      gender: "female",
      generation: 2,
      relationships: {
        parents: ["1", "4"],
        children: ["5"],
        spouses: [{ id: "6", startDate: "2000-03-20", endDate: null, current: true }],
        siblings: ["3"]
      },
      events: [
        { type: "birth", date: "1975-05-05", location: { place: "Los Angeles, USA" } },
        { type: "graduation", date: "1997-06-20", location: { place: "Stanford, USA" } },
        { type: "marriage", date: "2000-03-20", location: { place: "San Francisco, USA" } }
      ],
      children: [
        {
          id: "5",
          name: "Emily Smith",
          image: "/placeholders/emily.jpg",
          birthDate: "2005-11-12",
          birthPlace: { place: "San Francisco, USA", latitude: 37.7749, longitude: -122.4194 },
          deathDate: null,
          deathPlace: null,
          isAlive: true,
          gender: "female",
          generation: 3,
          relationships: {
            parents: ["2", "6"],
            children: [],
            spouses: [],
            siblings: []
          },
          events: [
            { type: "birth", date: "2005-11-12", location: { place: "San Francisco, USA" } }
          ],
          children: []
        }
      ]
    },
    {
      id: "3",
      name: "Jim Doe",
      image: "/placeholders/jim.jpg",
      birthDate: "1980-10-10",
      birthPlace: { place: "Chicago, USA", latitude: 41.8781, longitude: -87.6298 },
      deathDate: "2020-12-12",
      deathPlace: { place: "Miami, USA", latitude: 25.7617, longitude: -80.1918 },
      isAlive: false,
      gender: "male",
      generation: 2,
      relationships: {
        parents: ["1", "4"],
        children: [],
        spouses: [],
        siblings: ["2"]
      },
      events: [
        { type: "birth", date: "1980-10-10", location: { place: "Chicago, USA" } },
        { type: "graduation", date: "2002-05-15", location: { place: "New York, USA" } },
        { type: "death", date: "2020-12-12", location: { place: "Miami, USA" } }
      ],
      children: []
    }
  ]
};
```

## Step 5: Implement the Tree Visualization

Use D3.js to create a hierarchical tree visualization:

1. Set up the D3 tree layout:
   - Configure the tree layout with proper dimensions
   - Handle parent-child relationships
   - Support both vertical and horizontal orientations

2. Create interactive nodes:
   - Design the node component with all required information
   - Implement expand/collapse functionality
   - Add click handlers to focus on selected nodes
   - Show tooltips on hover with additional details

3. Add zoom and pan behavior:
   - Configure D3's zoom behavior
   - Set appropriate zoom extent (min/max)
   - Ensure smooth transitions
   - Add zoom controls (zoom in, zoom out, reset)

4. Implement relationship lines:
   - Draw parent-child connections
   - Style lines appropriately
   - Add marriage/partnership indicators
   - Highlight relationship paths between selected nodes

## Step 6: Style the Component

1. Create a StyledFamilyTree component using styled-components:
   - Responsive container sizing
   - Theme-based styling
   - Accessibility considerations

2. Design node styling:
   - Circular avatar containers
   - Status indicators
   - Typography for names and dates
   - Hover and selection states

3. Create global controls:
   - Material-UI buttons for expand/collapse all
   - Zoom controls with icons
   - Export button for SVG generation

## Step 7: Add Initial Tree Interactivity

1. Implement expand/collapse logic:
   - Toggle children visibility on click
   - Animate transitions
   - Update the tree layout after changes

2. Add focus navigation:
   - Center view on selected node
   - Implement smooth transition to new focus
   - Update breadcrumb trail if applicable

3. Create SVG export function:
   - Generate high-quality SVG of entire tree
   - Set up background processing for large trees
   - Add download functionality

Your initial implementation should handle all core tree visualization features while establishing a foundation for later integration of map views, person profiles, and other features. Focus on making the tree interaction smooth and intuitive, with a clean, modern UI that works well on both desktop and mobile devices.

## Implementation Guidelines

When implementing this component, focus on:
1. Clean, efficient code with proper TypeScript typing
2. Smooth, intuitive interactions with appropriate animations
3. Performance considerations for handling large family trees
4. Responsive design that works on various screen sizes
5. Accessibility features for all users

Start by implementing the core FamilyTree component and demonstrate the basic interactive functionality using the sample data provided above. We'll build out additional features once this foundation is in place.