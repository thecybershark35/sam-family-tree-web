# Family History Software Architecture

## Overview
A comprehensive web-based application for exploring and managing family histories through an interactive tree, geographical mapping, AI-driven data collection, and a conversational chatbot interface. The system allows users to visualize, explore, and collaborate on family trees with intuitive navigation and rich detail.

## Project Structure

```
samfamilytreeweb/
├── frontend/                    # React-based frontend
│   ├── public/                  # Static assets
│   │   ├── images/              # Default images and icons
│   │   └── index.html           # HTML entry point
│   ├── src/
│   │   ├── components/          # React components
│   │   │   ├── Authentication/  # Login/registration components
│   │   │   ├── FamilyTree/      # Tree visualization components
│   │   │   │   ├── FamilyTree.tsx           # Main tree component
│   │   │   │   ├── TreeNode.tsx             # Individual node component
│   │   │   │   ├── TreeControls.tsx         # Zoom/expand controls
│   │   │   │   ├── RelationshipStream.tsx   # Visual relationship links
│   │   │   │   └── SVGExport.tsx            # Tree export functionality
│   │   │   ├── MapView/        # Geographical components
│   │   │   │   ├── MapView.tsx              # Main map component
│   │   │   │   ├── LocationMarker.tsx       # Place markers
│   │   │   │   └── MigrationPath.tsx        # Migration visualization
│   │   │   ├── PersonProfile/  # Person detail components
│   │   │   │   ├── ProfileModal.tsx         # Modal container
│   │   │   │   ├── ProfileTabs.tsx          # Tab navigation
│   │   │   │   ├── OverviewTab.tsx          # Basic info tab
│   │   │   │   ├── CareerTab.tsx            # Career history tab
│   │   │   │   ├── MigrationTab.tsx         # Movement history tab
│   │   │   │   ├── RelationshipsTab.tsx     # Family connections tab
│   │   │   │   ├── PhotoGallery.tsx         # Photo management
│   │   │   │   └── CommentsSection.tsx      # Discussions
│   │   │   ├── Timeline/       # Chronological components
│   │   │   │   ├── Timeline.tsx             # Main timeline component
│   │   │   │   ├── EventFilters.tsx         # Filter controls
│   │   │   │   └── EventCard.tsx            # Individual events
│   │   │   ├── Chatbot/        # Conversational UI
│   │   │   │   ├── ChatInterface.tsx        # Chat component
│   │   │   │   └── CommandProcessor.tsx     # Process chat commands
│   │   │   └── Shared/         # Reusable components
│   │   │       ├── Button.tsx               # Custom buttons
│   │   │       ├── Modal.tsx                # Reusable modal
│   │   │       └── LoadingIndicator.tsx     # Loading states
│   │   ├── services/           # API integration
│   │   │   ├── api.ts                       # API client setup
│   │   │   ├── authService.ts               # Auth methods
│   │   │   ├── treeService.ts               # Tree data methods
│   │   │   ├── personService.ts             # Person data methods
│   │   │   ├── geocodingService.ts          # Location services
│   │   │   └── chatbotService.ts            # Dialogflow integration
│   │   ├── hooks/              # Custom React hooks
│   │   │   ├── useAuth.tsx                  # Authentication hook
│   │   │   ├── useTreeData.tsx              # Tree data hook
│   │   │   └── useGeocoding.tsx             # Geocoding hook
│   │   ├── contexts/           # React contexts
│   │   │   ├── AuthContext.tsx              # Auth state
│   │   │   └── FamilyTreeContext.tsx        # Tree state
│   │   ├── utils/              # Helper functions
│   │   │   ├── dateUtils.ts                 # Date formatting/calculation
│   │   │   ├── treeUtils.ts                 # Tree manipulation helpers
│   │   │   └── geocodingUtils.ts            # Location formatting
│   │   ├── types/              # TypeScript types
│   │   │   ├── Person.ts                    # Person interface
│   │   │   ├── Tree.ts                      # Tree structure interface
│   │   │   └── Event.ts                     # Timeline event interface
│   │   ├── assets/             # Frontend assets
│   │   ├── App.tsx             # Main app component
│   │   └── index.tsx           # React entry point
│   ├── .env                     # Environment variables (gitignored)
│   └── package.json             # Frontend dependencies
├── backend/                     # Node.js/Express API
│   ├── controllers/            # API logic
│   │   ├── authController.js                # Authentication endpoints
│   │   ├── treeController.js                # Family tree endpoints
│   │   ├── personController.js              # Person data endpoints
│   │   ├── photoController.js               # Photo upload/management
│   │   └── aiController.js                  # AI integration endpoints
│   ├── models/                 # Database models
│   │   ├── User.js                          # User model
│   │   ├── FamilyTree.js                    # Tree model
│   │   ├── Person.js                        # Person model
│   │   ├── Event.js                         # Event model
│   │   ├── Location.js                      # Location model
│   │   ├── Photo.js                         # Photo model
│   │   └── Comment.js                       # Comment model
│   ├── routes/                 # API endpoints
│   │   ├── authRoutes.js                    # Auth routes
│   │   ├── treeRoutes.js                    # Tree management routes
│   │   ├── personRoutes.js                  # Person data routes
│   │   ├── photoRoutes.js                   # Photo upload routes
│   │   └── aiRoutes.js                      # AI integration routes
│   ├── middleware/             # Express middleware
│   │   ├── auth.js                          # JWT authentication
│   │   ├── upload.js                        # File upload handling
│   │   └── validation.js                    # Request validation
│   ├── services/               # Business logic
│   │   ├── treeService.js                   # Tree operations
│   │   ├── geocodingService.js              # Location services
│   │   ├── aiScrapingService.js             # AI data collection
│   │   └── dialogflowService.js             # Chatbot integration
│   ├── utils/                  # Helper functions
│   │   ├── dateUtils.js                     # Date handling
│   │   ├── errorHandler.js                  # Error handling
│   │   └── treeUtils.js                     # Tree manipulation
│   ├── config/                 # Configuration
│   │   ├── database.js                      # Database connection
│   │   ├── auth.js                          # Auth configuration
│   │   └── storage.js                       # File storage config
│   ├── .env                     # Server environment variables (gitignored)
│   ├── app.js                   # Express server setup
│   └── package.json             # Backend dependencies
├── database/                    # Database setup
│   ├── migrations/              # Schema migrations
│   └── seeds/                   # Seed data
├── ai-scripts/                  # Python AI and scraping scripts
│   ├── scrapers/               # Web scrapers
│   │   ├── obituary_scraper.py             # Obituary data collection
│   │   ├── genealogy_scraper.py            # Genealogy site scraping
│   │   └── social_media_scraper.py         # Social data collection
│   ├── processors/             # Data processors
│   │   ├── text_processor.py               # NLP for extracted text
│   │   ├── relationship_extractor.py       # Find relationships in text
│   │   └── date_extractor.py               # Extract dates from text
│   ├── models/                 # ML models
│   │   └── person_matcher.py               # Identity matching
│   ├── utils/                  # Helper functions
│   │   ├── text_utils.py                   # Text processing utilities
│   │   └── data_cleaner.py                 # Data cleaning
│   ├── requirements.txt         # Python dependencies
│   └── README.md                # AI scripts documentation
├── docs/                        # Documentation
│   ├── api/                     # API documentation
│   ├── deployment/              # Deployment guides
│   └── user-guides/             # User manuals
├── .gitignore                   # Git ignore patterns
├── docker-compose.yml           # Docker configuration
└── README.md                    # Project overview and setup
```

## Components and Responsibilities

### 1. Frontend Layer
- **Authentication Module**: Manages user registration, login, and session management.
- **Family Tree Visualization**: Renders the interactive D3.js-based family tree with:
  - Collapsible/expandable nodes with proper spacing
  - Focus-based navigation (node becomes center when expanded)
  - Zoom and pan controls
  - Generation indicators
  - Relationship streams between nodes
  - SVG export functionality
- **Person Profile Module**: Displays comprehensive information about a selected person:
  - Multi-tab interface (Overview, Career, Migration, Relationships)
  - Photo gallery with upload capabilities
  - Comments/stories section
- **Geographical View**: Shows locations and migrations on a map:
  - Birth, death, and current locations as markers
  - Migration paths as connected lines
  - Filtering by person or time period
- **Timeline Module**: Chronological representation of family events:
  - Birth, death, marriage, and relocation events
  - Filtering by person, family branch, or event type
- **Chatbot Interface**: Natural language interaction:
  - Text input for queries and commands
  - Response display with visual feedback
  - Integration with tree navigation ("Show Bob's children")

### 2. Backend Layer
- **API Server**: RESTful endpoints for all frontend operations:
  - User authentication with JWT
  - CRUD operations for family trees, persons, and relationships
  - Photo upload and management
  - Chatbot integration
- **Business Logic Services**: Core application logic:
  - Tree manipulation (add/edit/delete nodes)
  - Relationship management
  - Permission checking
  - Data validation
- **Integration Services**: External service connections:
  - Geocoding service for location data
  - Dialogflow for chatbot functionality
  - AI system communication

### 3. Database Layer
- **User Management**: Stores user accounts and authentication data
- **Family Tree Structure**: Stores tree hierarchies and relationships
- **Person Data**: Detailed information about individuals
- **Event Data**: Temporal events (births, deaths, relocations)
- **Location Data**: Geographical information with coordinates
- **Media Storage**: Photos and other media files
- **Collaboration Data**: Comments, suggested edits, approvals

### 4. AI Subsystem
- **Web Scrapers**: Collect data from external sources:
  - Obituary websites
  - Genealogy databases
  - Public records
- **Natural Language Processing**: Extract structured data:
  - Identify people, relationships, dates, and locations
  - Match entities with existing records
  - Suggest additions/corrections to the tree
- **Admin Review Pipeline**: Present scraped data for approval:
  - Confidence scoring
  - Entity resolution
  - Duplicate detection

## Data Flow

### Authentication Flow
1. User registers/logs in → Frontend sends credentials → Backend validates
2. Backend generates JWT → Frontend stores token → Subsequent requests include token
3. Protected routes check token validity → Grant or deny access

### Family Tree Interaction Flow
1. User logs in → Backend returns list of accessible family trees
2. User selects a tree → Backend fetches tree data with permissions
3. Frontend renders tree using D3.js → User sees collapsed initial view
4. User interacts with tree (expand/collapse/zoom) → Frontend updates visualization
5. User clicks node → Frontend fetches detailed person data → Shows profile

### Profile Editing Flow
1. User views person profile → Clicks edit → Frontend shows edit form
2. User makes changes → Frontend validates → Sends to backend
3. Backend validates changes → Updates database → Returns success
4. Frontend updates UI to reflect changes

### Chatbot Interaction Flow
1. User types query ("Show me Bob's children") → Frontend sends to Dialogflow
2. Dialogflow identifies intent and entities → Backend processes request
3. Backend fetches relevant data → Returns to frontend
4. Frontend updates visualization (expands Bob's node, highlights children)

### AI Data Collection Flow
1. Admin initiates data collection → Backend triggers Python scripts
2. Scripts scrape sources → Process text with NLP → Extract structured data
3. Extracted data stored in review queue → Admin notified
4. Admin reviews via chatbot → Approves/rejects suggestions
5. Approved data integrated into family tree

## Performance Considerations

### Tree Rendering Optimization
- **Virtualization**: Only render visible portions of large trees
- **Level of Detail (LOD)**: Simplify visualization based on zoom level
  - Zoomed out: Simple nodes with minimal info
  - Zoomed in: Detailed nodes with all attributes
- **Lazy Loading**: Load branches on demand as they're expanded
- **Web Workers**: Offload complex layout calculations to background threads

### Large Tree Handling
- **Node Limit**: Target smooth performance up to ~2,000 nodes
- **SVG Export**: For very large trees:
  - Background processing with progress indicator
  - Email notification when export is complete
  - Downloadable high-resolution file
- **Tree Segmentation**: Break extremely large trees into manageable segments
  - Branch-based navigation
  - "Load more" functionality for distant relatives

### Database Performance
- **Indexing**: Optimize queries with proper indexes on:
  - Person IDs and names
  - Relationship types
  - Date fields
  - Location data
- **Caching**: Implement Redis caching for:
  - Frequently accessed trees
  - User permissions
  - Common queries

### API Optimization
- **Pagination**: Paginate large result sets
- **Partial Responses**: Return only necessary fields
- **Compression**: Enable GZIP/Brotli compression
- **Connection Pooling**: Reuse database connections

## Security Considerations

### Authentication & Authorization
- **JWT Security**: Short-lived tokens with refresh mechanism
- **Password Policy**: Strong password requirements
- **Rate Limiting**: Prevent brute force attacks
- **Role-Based Access**: Fine-grained permissions for:
  - Viewing trees
  - Editing person data
  - Approving changes
  - Adding new people

### Data Protection
- **API Security**: Input validation, CSRF protection
- **Secure Storage**: Encrypted sensitive data
- **HTTPS Only**: All communications encrypted
- **Privacy Controls**: User-defined sharing settings for family trees

### Media Security
- **Image Validation**: Verify uploaded files are safe images
- **Content Scanning**: Check for inappropriate content
- **Storage Security**: Secure access to uploaded files

## Scalability Strategy

### Horizontal Scaling
- **Stateless Design**: API servers can be scaled horizontally
- **Load Balancing**: Distribute traffic across multiple instances
- **Database Sharding**: Partition data for very large installations

### Vertical Scaling
- **Resource Optimization**: Efficient algorithms and queries
- **Memory Management**: Optimize for large tree handling
- **Upgrade Path**: Clear specifications for larger deployments

## Development Phases

### Phase 1: Authentication & Basic Tree
- User registration and login
- Basic family tree visualization
- Simple node details

### Phase 2: Advanced Tree Interaction
- Expand/collapse functionality
- Zoom and drag capabilities
- Generation indicators
- Relationship streams

### Phase 3: Person Profiles
- Detailed person view with tabs
- Photo upload functionality
- Comments/stories section

### Phase 4: Geographical Features
- Map integration
- Location markers
- Migration path visualization

### Phase 5: Timeline
- Chronological event display
- Filtering capabilities
- Visual event representation

### Phase 6: AI & Chatbot
- Chatbot interface
- Basic NLP capabilities
- Initial data scraping

### Phase 7: Advanced Features
- SVG export for large trees
- Analytics functionality
- Event planning helper
- Enhanced AI capabilities