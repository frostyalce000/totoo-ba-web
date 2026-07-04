# FDA Product Checker - Totoo Ba Ito?

License: MIT | TypeScript 5.9 | React 19.2 | Vite 7.1

A web application that helps Filipino consumers verify the authenticity and compliance of food, drug, and beauty products. The platform provides real-time verification against official FDA Philippines databases and business registries, helping protect consumers from counterfeit and unregistered products.

## Features

### Core Functionality

- **Dual Verification Methods**
  - **Text Search**: Search by product name, brand, or FDA registration number
  - **Image Upload**: AI-powered image verification using computer vision and OCR

- **Real-time Database Access**
  - Direct integration with FDA Philippines product databases
  - Cross-reference with Philippine Business Registry
  - Unified view of food products and pharmaceutical drugs

- **AI-Powered Matching**
  - Full-text search with PostgreSQL
  - Intelligent product matching algorithms
  - Image analysis for product verification

- **Counterfeit Detection**
  - Warnings for unregistered products
  - Verification status badges
  - Alternative product suggestions

- **Community Reporting**
  - Submit reports about suspicious or counterfeit products
  - Browse community-submitted reports
  - File upload support for evidence

### User Experience

- **Modern UI/UX**
  - Responsive design for mobile and desktop
  - Dark mode support
  - Accessible ARIA attributes throughout

- **Performance Optimized**
  - Lazy loading of routes and components
  - Code splitting for smaller bundle sizes
  - Virtualized product lists for large datasets
  - Optimized React Query caching
  - Server-side pagination with infinite scroll

- **Error Handling**
  - Comprehensive error boundaries
  - Structured domain errors with user-friendly messages
  - Graceful fallbacks

- **Maintenance Mode**
  - Optional maintenance page for deployments and updates
  - Enabled via environment variable

## Tech Stack

### Frontend

- **Framework**: React 19.2
- **Language**: TypeScript 5.9
- **Build Tool**: Vite 7.1
- **Styling**: Tailwind CSS 4.1
- **Routing**: React Router 7.9
- **State Management**: TanStack Query 5.90
- **Virtualization**: TanStack Virtual 3.13
- **Icons**: Lucide React
- **Theming**: next-themes

### Backend and Database

- **Database**: Supabase (PostgreSQL)
- **API**: RESTful API with image verification endpoint
- **Full-Text Search**: PostgreSQL tsvector for efficient searching

### Architecture

- **Domain Layer**: Business logic separated from UI and data access
- **Adapters**: Supabase and API adapters wired through a central registry
- **Query Hooks**: React Query hooks that delegate to domain modules

### Development Tools

- **Linter**: OXLint
- **Package Manager**: Bun (or npm/yarn)

## Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js**: v18 or higher
- **Bun**: Latest version (or npm/yarn as an alternative)
- **Git**: For cloning the repository

## Getting Started

### 1. Clone the Repository

```bash
git clone <repository-url>
cd totoo-ba-web
```

### 2. Install Dependencies

Using Bun (recommended):

```bash
bun install
```

Or using npm:

```bash
npm install
```

Or using yarn:

```bash
yarn install
```

### 3. Environment Configuration

Create a `.env` file in the root directory by copying the example:

```bash
cp .env.example .env
```

Then configure the following environment variables:

```env
# Supabase Configuration
VITE_SUPABASE_URL=your_supabase_project_url
VITE_SUPABASE_PUBLISHABLE_KEY=your_supabase_anon_key

# API Configuration (for image verification)
VITE_API_BASE_URL=your_api_base_url

# Optional: Maintenance Mode
VITE_MAINTENANCE_MODE=false
```

**Getting Supabase Credentials:**

1. Create a free account at Supabase
2. Create a new project
3. Go to Project Settings > API
4. Copy the Project URL and anon/public key

Set `VITE_MAINTENANCE_MODE=true` to show the maintenance page instead of the full application.

### 4. Database Setup

The application requires the following Supabase tables:

- `food_products` - FDA-registered food products
- `drug_products` - FDA-registered pharmaceutical products
- `unified_products` - Database view combining both tables
- `food_industry` - Business registry for food manufacturers
- `drug_industry` - Business registry for drug manufacturers

Refer to `create_unified_products_view.sql` for the database schema.

### 5. Start Development Server

```bash
bun run dev
```

The application will be available at `http://localhost:5173`

## Available Scripts

| Command | Description |
|---------|-------------|
| `bun run dev` | Starts the development server with hot reload |
| `bun run build` | Builds the application for production |
| `bun run lint` | Lints the codebase using OXLint |
| `bun run preview` | Previews the production build locally |
| `bun run check` | Runs lint and build together |

## Usage Guide

### Text Search Verification

1. Navigate to the homepage
2. Ensure the "Text Search" tab is selected
3. Enter the product name, brand, or FDA registration number
4. (Optional) Select a product category (Food, Drugs, Cosmetics)
5. Click "Verify Product"
6. View verification results including registration status, product details, manufacturer information, registration and expiry dates, and alternative matches

### Image Verification

1. Navigate to the homepage
2. Click the "Image Upload" tab
3. Click to upload or drag and drop a product image
4. Supported formats: WEBP, PNG, JPG
5. Click "Verify Product Image"
6. Wait for AI analysis (typically 3–5 seconds)
7. View extracted information and verification results

### Browse Products

1. Click "Products" in the navigation
2. Use filters to narrow results by category
3. Use the search bar for specific products
4. Click "Load More" to view additional products
5. Click the eye icon on any product card for detailed information

### View Analytics

1. Click "Analytics" in the navigation
2. View statistics including total registered products, products by category, database coverage, and recent updates

### Submit a Product Report

1. Click "Report" in the navigation
2. Fill in product details and describe the issue
3. (Optional) Upload supporting images
4. Submit the report for review

### Browse Community Reports

1. Click "Community Reports" in the navigation
2. View reports submitted by other users
3. Click a report to see full details

## Project Structure

```
totoo-ba-web/
├── public/                    # Static assets
├── src/
│   ├── assets/               # Images and static files
│   ├── components/           # React components
│   ├── db/                   # Database configuration
│   │   └── supabaseClient.ts
│   ├── domain/               # Business logic and adapters
│   │   ├── adapters/         # Supabase and API adapters
│   │   ├── adapterRegistry.ts
│   │   ├── productListing.ts
│   │   ├── productVerification.ts
│   │   ├── imageVerification.ts
│   │   ├── communityReport.ts
│   │   ├── productReport.ts
│   │   └── analyticsDataAccess.ts
│   ├── hooks/                # Custom React hooks
│   ├── pages/                # Route pages
│   │   ├── About.tsx
│   │   ├── Analytics.tsx
│   │   ├── CommunityReports.tsx
│   │   ├── Maintenance.tsx
│   │   ├── NotFound.tsx
│   │   ├── Products.tsx
│   │   ├── Report.tsx
│   │   └── Verify.tsx
│   ├── query/                # React Query hooks
│   │   ├── get/              # GET request hooks
│   │   └── post/             # POST request hooks
│   ├── types/                # TypeScript type definitions
│   ├── utils/                # Utility functions
│   ├── App.tsx               # Root layout component
│   ├── main.tsx              # Application entry point
│   └── index.css             # Global styles
├── .env.example              # Environment variables template
├── create_unified_products_view.sql
├── package.json
├── tsconfig.json
├── vite.config.ts
└── README.md
```

## Configuration Files

### Vite Configuration (`vite.config.ts`)

- React plugin with Fast Refresh
- Tailwind CSS integration
- Code splitting for vendor libraries
- Build optimizations for production

### TypeScript Configuration (`tsconfig.json`)

- Strict type checking enabled
- Modern ES module support
- Path aliases for cleaner imports

### Tailwind Configuration (`tailwind.config.js`)

- Custom color scheme
- Dark mode support
- Responsive breakpoints

## Component Documentation

All components are documented with JSDoc comments. Key components include:

- **SearchForm**: Dual-method product verification form
- **ProductCard**: Displays product information with verification status
- **VirtualProductList**: Virtualized list for large product catalogs
- **ErrorBoundary**: Catches and handles React errors gracefully
- **Navbar**: Responsive navigation with mobile menu
- **Hero**: Landing page hero section
- **Features**: Feature showcase grid

See inline documentation in each component file for detailed usage.

## API Integration

### Supabase Queries

The application uses React Query hooks that delegate to domain modules:

- `useGetUnifiedProductsQuery` - Infinite scroll product list
- `useGetProductVerifyQuery` - Single product verification
- `useGetAnalyticsQuery` - Database statistics
- `useGetReportsQuery` - Community reports listing
- `usePostVerifyImage` - Image verification mutation

### Image Verification API

Endpoint: `POST /api/v1/products/new-verify-image`

- Accepts: multipart/form-data with image file
- Returns: Verification result with AI analysis

## Contributing

Contributions are welcome. Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

Please ensure your code:

- Follows the existing code style
- Includes appropriate documentation
- Passes linting (`bun run lint`)
- Builds successfully (`bun run build`)

## License

This project is licensed under the MIT License. See the LICENSE file for details.

## Acknowledgments

- FDA Philippines for providing public access to product databases
- Philippine Business Registry for business verification data
- Open source community for the tools and libraries used in this project

## Support

For issues, questions, or suggestions, open an issue on the project repository or check the documentation in the codebase.

## Future Enhancements

- [ ] Barcode scanning functionality
- [ ] User accounts and saved searches
- [ ] Product comparison features
- [ ] Email notifications for expiring registrations
- [ ] Multi-language support (English, Filipino)
- [ ] Offline mode with cached data

---

Made with care for Filipino consumers
