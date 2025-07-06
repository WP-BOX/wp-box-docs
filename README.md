## Docs

Bedrock for Wordpress: https://github.com/roots/bedrock  
PostgreSQL for Wordpress: https://github.com/PostgreSQL-For-Wordpress/postgresql-for-wordpress.git  
Documentation Wordpress: https://developer.wordpress.org/  
Documentation Tailwind: https://tailwindcss.com/docs/installation  

## Installation

Make sure to have git, docker, docker-compose on your system:
```
sudo apt-get install docker docker-compose git make
```

Find your user id and group id for usage in the next command
```
id -u
id -g
```

Create a directory /var/www/your.domain owned by non-root user and enter it
```
sudo mkdir -p /var/www/your.domain
sudo -u $(whoami) chown -R <USER_ID>:<GROUP_ID> /var/www/your.domain
```

Cd into that directory and clone the project from wp-box repository, or your version
```
cd /var/www/your.domain
git init .
git remote add -t \* -f origin git@github.com:WP-BOX/wp-box.git
git checkout master
```

Add your user to docker group
```
sudo usermod -a -G docker $(whoami)
```

Copy .env file and add change variables there:
```
cp .env.example .env
```

Run install script:
```
make install-all
```

Run docker environment (if already installed):
```
make docker-up
```

Verify all containers have started with:
```
docker ps
```

Run composer install && wp cli scripts:
```
make post-install
```

Visit https://<SITE_DOMAIN> in browser, or if you changed domain in .env visit that domain.
Note that you might need additional DNS setup or /etc/hosts setup for custom domains.

## Patching

Some dependencies might need patching, consider:
```
git diff --no-index oldfile newfile > patches/savefile.patch
```
And add the patch in composer.json

## Blocks

### Account Form Block
A comprehensive authentication modal featuring login, registration, and password recovery forms with social login integration (Google, Yandex). Includes form validation, password confirmation, and consent checkboxes for privacy policy and terms of service. This modal is toggled by the [Account Switcher Block](#account-switcher-block).

#### Path: `web/app/themes/wp-box/blocks/account-form/`
#### Tags: Authentication, Modal, Social Login

### Account Reset Password Block
A specialized password reset interface for setting a new password after users have confirmed their reset intent via email. This block handles the final step of password recovery, while the initial password reset request is handled by the [Account Form Block](#account-form-block).

#### Path: `web/app/themes/wp-box/blocks/account-reset-password/`
#### Tags: Authentication, Password Recovery

### Account Switcher Block
A toggle button for account authentication functions, providing easy access to login/logout functionality and account management interface. Opens the [Account Form Block](#account-form-block) modal for user authentication.

#### Path: `web/app/themes/wp-box/blocks/account-switcher/`
#### Tags: Authentication, User Interface

### Author Contacts Block
Displays author contact links with icons for phone, WhatsApp, and Telegram. Automatically extracts contact information from author user metadata of the current post or viewed author. Features styled SVG icons and proper links for each contact type.

#### Path: `web/app/themes/wp-box/blocks/author-contacts/`
#### Tags: Author Management, Contact Information, Social Links

### Author Profile Block
Displays basic author profile information including the display name as a heading. For authenticated users (profile owner or users with editing rights), provides AJAX logout functionality. Automatically determines the author from URL parameters or global variables.

#### Path: `web/app/themes/wp-box/blocks/author-profile/`
#### Tags: Author Management, User Profile, AJAX Functionality

### Author Purchases Block
Displays a structured list of products or items purchased by authors, providing purchase history and transaction information for author profiles.

#### Path: `web/app/themes/wp-box/blocks/author-purchases/`
#### Tags: Author Management, E-commerce, Purchase History

### Author Subscription Block
A subscription management interface for authenticated users (profile owner or editors) that displays subscription details including subscription products, expiry dates, and functionality to resend GitHub invitations or subscribe to products. Automatically determines the author and displays only active subscription products.

#### Path: `web/app/themes/wp-box/blocks/author-subscription/`
#### Tags: Author Management, Subscription Management, GitHub Integration

### Breadcrumbs Block
A schema.org-compliant navigation breadcrumb system that displays hierarchical page structure. Automatically generates breadcrumbs based on page relationships, post types, and taxonomies with multilingual support.

#### Path: `web/app/themes/wp-box/blocks/breadcrumbs/`
#### Tags: Navigation, SEO, Schema Markup

### Button Block
A flexible button component with alignment controls and customizable styling. Supports various button types and positioning options within content layouts.

#### Path: `web/app/themes/wp-box/blocks/button/`
#### Tags: UI Elements, Interactive Components

### Card Block
Displays content in structured card layouts with media support. Ideal for showcasing featured content, product previews, or article summaries with consistent formatting.

#### Path: `web/app/themes/wp-box/blocks/card/`
#### Tags: Content Display, Layout, Media

### Flex Columns Block
Creates responsive multi-column layouts using CSS flexbox. Provides dynamic column arrangement with automatic responsive behavior for optimal content organization.

#### Path: `web/app/themes/wp-box/blocks/flex-columns/`
#### Tags: Layout, Responsive Design, Flexbox

### Footer Block
Generates site-wide footer components with customizable content areas, links, and branding elements. Essential for consistent site navigation and information.

#### Path: `web/app/themes/wp-box/blocks/footer/`
#### Tags: Site Structure, Navigation, Branding

### GitHub Button Block
Interactive GitHub integration block that provides AJAX-powered repository access management. Allows users to request GitHub repository invitations, handles automatic user lookup by email, manages organization memberships, and adds collaborators to private repositories. Integrates with subscription validation and provides real-time feedback for GitHub API operations.
#### Path: `web/app/themes/wp-box/blocks/github-button/`
#### Tags: GitHub Integration, Repository Access, AJAX, Subscription Management

### Group Block
A container block for grouping and organizing other blocks with shared styling and layout properties.

#### Path: `web/app/themes/wp-box/blocks/group/`
#### Tags: Layout, Container, Organization

### Header Block
Main site header component supporting complex layouts with navigation menus, branding, and interactive elements. Non-reusable block for consistent site identity.

#### Path: `web/app/themes/wp-box/blocks/header/`
#### Tags: Site Structure, Navigation, Branding

### Header Left Block
Left section component of the header layout, typically containing logos, branding elements, or primary navigation items.

#### Path: `web/app/themes/wp-box/blocks/header-left/`
#### Tags: Header Components, Navigation, Branding

### Header Menu Block
Navigation menu component designed for header integration. Provides structured menu display with responsive behavior.

#### Path: `web/app/themes/wp-box/blocks/header-menu/`
#### Tags: Navigation, Menu System, Header Components

### Header Right Block
Right section component of the header layout, commonly used for user actions, search, theme switcher, and secondary navigation elements.

#### Path: `web/app/themes/wp-box/blocks/header-right/`
#### Tags: Header Components, User Actions, Utilities

### Heading Section Block
Large headline sections with advanced styling options including background positioning and text alignment. Perfect for page headers and section dividers.

#### Path: `web/app/themes/wp-box/blocks/heading-section/`
#### Tags: Typography, Section Headers, Visual Hierarchy

### Hero Section Block
A specialized homepage hero banner with customizable background colors. Designed as a unique, non-reusable block for prominent page introductions.

#### Path: `web/app/themes/wp-box/blocks/hero-section/`
#### Tags: Homepage, Hero Banner, Featured Content

### Image Block
Advanced responsive image component that generates optimized `<picture>` elements with multiple breakpoints, automatic WebP format conversion, and performance optimizations. Features lazy loading, object-fit controls, custom dimensions, caption support, and intelligent caching. Supports JPG/PNG (with WebP fallbacks), GIF, and SVG formats with responsive srcset generation for optimal loading across devices.

#### Path: `web/app/themes/wp-box/blocks/image/`
#### Tags: Media, Responsive Images, WebP Optimization, Performance

### Language Settings Block
Configuration interface for language preferences and multilingual site settings. Works in conjunction with the language switcher for internationalization.

#### Path: `web/app/themes/wp-box/blocks/language-settings/`
#### Tags: Internationalization, Configuration, Language Management

### Language Switcher Block
Interactive language selector displaying current language with icon. Triggers a modal for language selection on multilingual sites with proper translations support.

#### Path: `web/app/themes/wp-box/blocks/language-switcher/`
#### Tags: Internationalization, Language Selection, Modal

### Menu Switcher Block
Navigation component that enables switching between different menu display modes or menu types within the site interface.

#### Path: `web/app/themes/wp-box/blocks/menu-switcher/`
#### Tags: Navigation, Menu System, Interface Control

### Page Menu Block
Contextual navigation menu for page-specific navigation. Provides local navigation between page headings.

#### Path: `web/app/themes/wp-box/blocks/page-menu/`
#### Tags: Page Navigation, Local Navigation, Content Structure

### Payment Button Block
E-commerce payment initiation button with product integration. Displays pricing information from product metadata and supports multiple payment providers with custom pricing options.

#### Path: `web/app/themes/wp-box/blocks/payment-button/`
#### Tags: E-commerce, Payments, Product Integration

### Payment Form Button Block
Enhanced payment interface component providing structured checkout processes with form validation and payment method selection.

#### Path: `web/app/themes/wp-box/blocks/payment-form-button/`
#### Tags: E-commerce, Payment Processing, Form Interface

### Post Link Block
Creates formatted links to posts with enhanced visual styling and metadata display for better content discovery and navigation.

#### Path: `web/app/themes/wp-box/blocks/post-link/`
#### Tags: Content Links, Post Navigation, Content Discovery

### Product Price Block
Displays formatted product pricing information with currency symbols and styling. Integrates with product data for dynamic price display.

#### Path: `web/app/themes/wp-box/blocks/product-price/`
#### Tags: E-commerce, Product Information, Pricing

### Product Taxonomies Block
Displays categorized product information based on taxonomies and product classifications. Essential for e-commerce product organization and filtering.

#### Path: `web/app/themes/wp-box/blocks/product-taxonomies/`
#### Tags: E-commerce, Product Categories, Taxonomy Display

### Queried Object Template Block
Dynamic template rendering system that formats content based on current query context. Conditionally displays templates for posts, terms, users, and other WordPress objects.

#### Path: `web/app/themes/wp-box/blocks/queried-object-template/`
#### Tags: Dynamic Content, Template System, Conditional Display

### Search Form Block
Modal-based search interface with advanced search functionality. Includes post type filtering, language-specific search, and user-friendly form validation.

#### Path: `web/app/themes/wp-box/blocks/search-form/`
#### Tags: Search Functionality, Modal Interface, Content Discovery

### Search Switcher Block
Toggle component for activating search interfaces and switching between different search modes or contexts within the site.

#### Path: `web/app/themes/wp-box/blocks/search-switcher/`
#### Tags: Search Interface, Toggle Controls, User Interface

### Section Block
Modular content sections with comprehensive styling controls including background management, alignment options, and spacing controls for flexible page layouts.

#### Path: `web/app/themes/wp-box/blocks/section/`
#### Tags: Layout Sections, Content Organization, Styling Controls

### Section Menu Block
Navigation menu specifically designed for navigation between different content with a single section. Doesn't work together with page menu.

#### Path: `web/app/themes/wp-box/blocks/section-menu/`
#### Tags: Section Navigation, Horizontal Menus, Content Organization

### Simple Gallery Block
Basic image gallery component with configurable layouts and display options for showcasing multiple images in an organized format.

#### Path: `web/app/themes/wp-box/blocks/simple-gallery-example/`
#### Tags: Image Gallery, Media Display, Visual Content

### SVG Block
Enables dynamic embedding and styling of SVG graphics with customizable attributes for scalable vector graphics integration throughout the site.

#### Path: `web/app/themes/wp-box/blocks/svg/`
#### Tags: Vector Graphics, SVG Integration, Scalable Graphics

### Theme Settings Block
Configuration interface for theme-wide parameters and customization options. Provides centralized theme management functionality. This modal is toggled by the [Theme Switcher Block](#theme-switcher-block).

This block is designed to be used in footer template part.

#### Path: `web/app/themes/wp-box/blocks/theme-settings/`
#### Tags: Theme Configuration, Settings Management, Customization

### Theme Switcher Block
Interactive theme selection button that toggles theme settings modal. Features a visual theme icon and integrates with the [Theme Settings Block](#theme-settings-block) for real-time theme switching.

This block is designed to be added as a button in desktop / mobile header.

#### Path: `web/app/themes/wp-box/blocks/theme-switcher/`
#### Tags: Theme Selection, Visual Customization, User Preferences

## Core Blocks Overrides

### Avatar Block Override
WordPress core avatar block enhanced with performance optimizations and Tailwind CSS styling. Adds lazy loading, low fetch priority, and async decoding attributes to avatar images, plus rounded corners styling for consistent design integration.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/avatar/`
#### Core Block: [WordPress Avatar Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/avatar)

### Button Block Override
WordPress core button block completely unregistered and disabled. The theme provides its own custom button implementation through the [Button Block](#button-block) for enhanced styling control and better integration with the theme's design system.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/button/`
#### Core Block: [WordPress Button Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/button)

### Code Block Override
WordPress core code block enhanced with custom editor interface and language support. Removes default typography, spacing, and color controls, adds custom code language and file name attributes, and provides a styled code editor interface with window chrome and syntax highlighting preview.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/code/`
#### Core Block: [WordPress Code Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/code)

### Details Block Override
WordPress core details block completely unregistered and disabled. The theme removes this accordion-style block in favor of custom implementation or alternative content organization methods.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/details/`
#### Core Block: [WordPress Details Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/details)

### Footnotes Block Override
WordPress core footnotes block completely unregistered and disabled. The theme removes this block in favor of alternative footnote implementations or content organization methods.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/footnotes/`
#### Core Block: [WordPress Footnotes Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/footnotes)

### Gallery Block Override
WordPress core gallery block completely unregistered and disabled. The theme provides its own gallery implementation through the [Simple Gallery Block](#simple-gallery-block) for better control over layout and styling.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/gallery/`
#### Core Block: [WordPress Gallery Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/gallery)

### Group Block Override
WordPress core group block completely unregistered and disabled. The theme provides its own container implementation through the [Group Block](#group-block) for enhanced layout capabilities with custom Tailwind classes.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/group/`
#### Core Block: [WordPress Group Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/group)

### Heading Block Override
WordPress core heading block enhanced with custom Tailwind font size controls. Removes default typography supports and adds tailwindFontSize attribute with responsive heading classes (heading/big-heading) for consistent typography hierarchy. Also applies Tailwind classes to frontend output.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/heading/`
#### Core Block: [WordPress Heading Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/heading)

### List Block Override
WordPress core list block modified with Tailwind CSS styling controls. Removes default spacing and color supports, adds custom Tailwind classes for consistent list styling with proper spacing, typography, and list markers (decimal for ordered, square for unordered).

#### Path: `web/app/themes/wp-box/blocks-overrides/core/list/`
#### Core Block: [WordPress List Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/list)

### List Item Block Override
WordPress core list item block enhanced with Tailwind CSS integration. 

#### Path: `web/app/themes/wp-box/blocks-overrides/core/list-item/`
#### Core Block: [WordPress List Item Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/list-item)

### Media Text Block Override
WordPress core media and text block completely unregistered and disabled. This block is removed for now as it requires additional changes.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/media-text/`
#### Core Block: [WordPress Media Text Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/media-text)

### More Block Override
WordPress core "read more" block completely unregistered and disabled. This block is removed for now as it requires additional changes.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/more/`
#### Core Block: [WordPress More Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/more)

### Navigation Block Override
WordPress core navigation block enhanced with Tailwind CSS styling. Applies custom classes for consistent navigation appearance and responsive behavior while maintaining core navigation functionality.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/navigation/`
#### Core Block: [WordPress Navigation Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/navigation)

### Navigation Link Block Override
WordPress core navigation link block enhanced with Tailwind CSS link styling. Applies custom classes for consistent navigation item appearance that integrates with the theme's design system.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/navigation-link/`
#### Core Block: [WordPress Navigation Link Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/navigation-link)

### Next Page Block Override
WordPress core page break block completely unregistered and disabled. This block is removed for now as it requires additional changes.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/nextpage/`
#### Core Block: [WordPress Next Page Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/nextpage)

### Paragraph Block Override
WordPress core paragraph block enhanced with custom Tailwind font size controls. Removes default typography, spacing, and color supports, adds tailwindFontSize attribute with responsive paragraph classes (sm/base) and theme-consistent text colors for both editor and frontend.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/paragraph/`
#### Core Block: [WordPress Paragraph Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/paragraph)

### Post Author Biography Block Override
WordPress core post author biography block enhanced with Tailwind CSS styling. Applies custom typography and spacing classes for consistent author bio presentation that integrates with the theme's design system.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/post-author-biography/`
#### Core Block: [WordPress Post Author Biography Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/post-author-biography)

### Post Author Name Block Override
WordPress core post author name block enhanced with Tailwind CSS typography controls. Applies custom heading classes for consistent author name styling across different post contexts and layouts.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/post-author-name/`
#### Core Block: [WordPress Post Author Name Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/post-author-name)

### Post Content Block Override
WordPress core post content block enhanced with Tailwind CSS container styling. Applies custom wrapper classes for consistent content area layout and proper spacing within post templates.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/post-content/`
#### Core Block: [WordPress Post Content Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/post-content)

### Post Excerpt Block Override
WordPress core post excerpt block enhanced with Tailwind CSS styling. Applies custom typography and spacing classes for consistent excerpt presentation that matches the theme's design system.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/post-excerpt/`
#### Core Block: [WordPress Post Excerpt Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/post-excerpt)

### Post Navigation Link Block Override
WordPress core post navigation link block enhanced with Tailwind CSS link styling. Applies custom classes for consistent navigation between posts with enhanced visual design and proper spacing.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/post-navigation-link/`
#### Core Block: [WordPress Post Navigation Link Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/post-navigation-link)

### Post Title Block Override
WordPress core post title block enhanced with Tailwind CSS heading controls. Applies custom heading classes for consistent post title typography that integrates with the theme's heading hierarchy and responsive design.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/post-title/`
#### Core Block: [WordPress Post Title Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/post-title)

### Preformatted Block Override
WordPress core preformatted text block completely unregistered and disabled. The theme removes this block in favor of the enhanced [Code Block Override](#code-block-override) for better code and preformatted text presentation.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/preformatted/`
#### Core Block: [WordPress Preformatted Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/preformatted)

### Pull Quote Block Override
WordPress core pull quote block completely unregistered and disabled. The theme removes this block in favor of alternative quote styling solutions or the standard [Quote Block Override](#quote-block-override).

#### Path: `web/app/themes/wp-box/blocks-overrides/core/pullquote/`
#### Core Block: [WordPress Pull Quote Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/pullquote)

### Query Block Override
WordPress core query loop block enhanced with Tailwind CSS layout controls. Applies custom classes for responsive post query display with consistent grid and list layouts using the theme's design system.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/query/`
#### Core Block: [WordPress Query Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/query)

### Query Pagination Block Override
WordPress core query pagination block enhanced with Tailwind CSS pagination styling. Applies custom classes for consistent pagination controls with responsive design and proper theme integration.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/query-pagination/`
#### Core Block: [WordPress Query Pagination Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/query-pagination)

### Query Pagination Next Block Override
WordPress core pagination next button block enhanced with Tailwind CSS button styling. Applies custom classes for consistent forward navigation controls that match the theme's button design system.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/query-pagination-next/`
#### Core Block: [WordPress Query Pagination Next Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/query-pagination-next)

### Query Pagination Numbers Block Override
WordPress core pagination numbers block enhanced with Tailwind CSS styling. Applies custom classes for numbered pagination controls that match the theme's button and link styling with proper spacing and responsive behavior.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/query-pagination-numbers/`
#### Core Block: [WordPress Query Pagination Numbers Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/query-pagination-numbers)

### Query Pagination Previous Block Override
WordPress core pagination previous button block enhanced with Tailwind CSS button styling. Applies custom classes for consistent backward navigation controls that complement the pagination system design.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/query-pagination-previous/`
#### Core Block: [WordPress Query Pagination Previous Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/query-pagination-previous)

### Query Title Block Override
WordPress core query title block enhanced with Tailwind CSS heading controls. Applies custom heading classes for consistent archive and search result title styling with responsive typography that matches the theme's hierarchy.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/query-title/`
#### Core Block: [WordPress Query Title Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/query-title)

### Quote Block Override
WordPress core quote block completely unregistered and disabled. This block is removed for now as it requires additional changes.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/quote/`
#### Core Block: [WordPress Quote Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/quote)

### Separator Block Override
WordPress core separator block completely unregistered and disabled. This block is removed for now as it requires additional changes.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/separator/`
#### Core Block: [WordPress Separator Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/separator)

### Spacer Block Override
WordPress core spacer block completely unregistered and disabled. This block is removed for now as it requires additional changes.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/spacer/`
#### Core Block: [WordPress Spacer Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/spacer)

### Table Block Override
WordPress core table block completely unregistered and disabled. This block is removed for now as it requires additional changes.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/table/`
#### Core Block: [WordPress Table Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/table)

### Verse Block Override
WordPress core verse block completely unregistered and disabled. This block is removed for now as it requires additional changes.

#### Path: `web/app/themes/wp-box/blocks-overrides/core/verse/`
#### Core Block: [WordPress Verse Block](https://github.com/WordPress/gutenberg/tree/trunk/packages/block-library/src/verse)