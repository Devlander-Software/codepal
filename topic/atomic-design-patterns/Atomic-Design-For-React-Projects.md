

# **Component Folder Structure Documentation**

This document serves as a detailed guide to the folder structure used for organizing UI components in the project. It explains the reasoning behind the structure, defines the roles of each folder, and provides guidelines on where and how to add new components. The aim is to ensure clarity, scalability, and consistency across the codebase.

---

## **Philosophy Behind the Folder Structure**

This structure is based on the **Atomic Design methodology**, a design system that emphasizes building UI elements in a hierarchical manner:

1. **Atoms**: The foundational building blocks of the UI.
2. **Molecules**: Groups of atoms that form small, reusable components.
3. **Organisms**: Larger sections composed of molecules and atoms, representing distinct areas of the UI.
4. **Templates**: Page layouts combining organisms, molecules, and atoms to create reusable structures.

Additionally, this structure considers **modern development needs** such as scalability, modularity, and ease of collaboration. It ensures components are reusable, discoverable, and organized logically.

---

## **Folder Overview**

### **src/components**

```
src/components/
├── atoms/
├── molecules/
├── organisms/
└── templates/
```

Each folder represents a specific level of UI complexity, ensuring that components are grouped logically and hierarchically.

---

## **Folder Breakdown**

### **1. Atoms**

Atoms are the simplest UI components. They are single-purpose elements that cannot be broken down further in terms of UI functionality. Atoms are highly reusable and are often the building blocks for molecules and organisms.

#### **Purpose**
- Serve as the foundation for the design system.
- Represent single, reusable UI elements.

#### **Subfolders**
1. **basic**: Core elements like buttons, text, images, and icons.
   - Example components: `BaseText`, `BaseImage`, `TextButton`
2. **containers**: Simple layout and structural components.
   - Example components: `PaddingContainer`, `SafeAreaViewContainer`
3. **feedback**: Components for user notifications or statuses.
   - Example components: `Badge`, `PulsatingBadge`
4. **layout**: Spacing and layout utilities.
   - Example components: `Divider`, `Spacer`
5. **decorations**: Visual or decorative elements.
   - Example components: `BaseGradient`, `LogoSVG`

#### **Examples**
- `TextButton`: A single-purpose button.
- `Divider`: A visual divider between sections.
- `PulsatingBadge`: A feedback element indicating activity.

---

### **2. Molecules**

Molecules combine two or more atoms to create more complex components. These components often represent small, functional parts of the UI, like form inputs or cards.

#### **Purpose**
- Combine atoms into more meaningful UI elements.
- Add interactivity or more specific functionality to atoms.

#### **Subfolders**
1. **inputs**: Form-related components.
   - Example components: `CheckboxInputGroup`, `RoundedInput`
2. **cards**: Encapsulated containers of information.
   - Example components: `MediaCard`, `TileCardContainer`
3. **lists**: List-related components.
   - Example components: `ListItem`, `BaseSectionList`
4. **navigation**: Interactive navigation components.
   - Example components: `TabBarIcon`, `LeafShapedTab`
5. **buttons**: Complex button designs.
   - Example components: `CircleButton`, `PillButton`

#### **Examples**
- `MediaCard`: Displays an image, title, and description in a card format.
- `RoundedInput`: A text input field with a specific rounded design.
- `TabBarIcon`: A navigation icon for tab bars.

---

### **3. Organisms**

Organisms are larger, reusable sections of the UI. They often represent distinct, self-contained parts of a page. Organisms typically combine multiple molecules and atoms.

#### **Purpose**
- Represent complex, reusable UI sections.
- Serve as building blocks for templates and layouts.

#### **Subfolders**
1. **headers**: Components for page or modal headers.
   - Example components: `MainHeader`, `ModalHeader`
2. **footers**: Footer-related components.
   - Example components: `FixedFooter`, `LandingSplashFooter`
3. **content**: Content-heavy components.
   - Example components: `FeatureList`, `ReferencesSection`
4. **navigation**: Larger navigational units.
   - Example components: `Sidebar`, `DrawerMenu`
5. **interactive**: Highly interactive components.
   - Example components: `ScrollableCarousel`, `SectionListSearchBar`

#### **Examples**
- `FeatureList`: Displays a list of features, often with icons and descriptions.
- `MainHeader`: A header component with a title, navigation controls, and optional actions.
- `ScrollableCarousel`: A horizontal scrolling carousel for showcasing items.

---

### **4. Templates**

Templates define high-level layouts and page structures. They combine organisms, molecules, and atoms to create reusable page templates.

#### **Purpose**
- Provide a structural blueprint for pages.
- Represent reusable layouts for specific page types.

#### **Subfolders**
1. **marketing**: Templates for marketing-focused pages.
   - Example components: `LandingSplash`, `ProductShowcase`
2. **dashboard**: Templates for dashboard-like pages.
   - Example components: `UserDashboard`, `AdminPanel`
3. **forms**: Templates for input-heavy pages.
   - Example components: `SignupForm`, `SurveyPage`

#### **Examples**
- `LandingSplash`: A marketing page layout with a hero section, features, and a call to action.
- `UserDashboard`: A dashboard layout for authenticated users, including navigation and content sections.

---

## **Guidelines for Adding Components**

### **1. Determine the Component's Role**
- **Atom**: Single-purpose UI element with no dependencies.
- **Molecule**: Combines atoms for specific functionality.
- **Organism**: A larger, reusable section combining molecules and atoms.
- **Template**: A high-level page layout.

### **2. Use the Appropriate Subfolder**
- **Purpose**: Place the component in the folder that aligns with its primary role (e.g., `feedback`, `navigation`).
- **Reusability**: Components designed for repeated use across pages belong in atoms, molecules, or organisms.

### **3. Follow Naming Conventions**
- Use **PascalCase** for component names (e.g., `TileCardContainer`).
- Avoid abbreviations unless they are widely understood (e.g., `SVG`, `CTA`).

### **4. Write Documentation**
- Include a comment in the component file to describe its purpose, props, and usage.

### **5. Update Dependencies**
- Ensure new components are tested and integrated into Storybook (or equivalent).

---

## **FAQs**

### **Why is this structure used?**
This structure ensures components are modular, scalable, and easy to understand. By aligning with the Atomic Design methodology, the codebase becomes consistent and maintainable.

### **What if a component doesn’t fit neatly into an existing category?**
Consider creating a new subfolder that aligns with the component's purpose. For example, add a `charts` subfolder under molecules for graph-related components.

### **How do I know if a component is a molecule or organism?**
- Molecule: A small, reusable component combining a few atoms (e.g., `CheckboxInputGroup`).
- Organism: A larger section combining molecules to form a distinct part of the UI (e.g., `MainHeader`).

### **Where do utility components go?**
Utility components that are not tied to UI (e.g., context providers, HOCs) belong outside this folder, in a `utils` or `context` folder.

---

## **Future Scalability**

This structure is designed to grow with the project. As new types of components are introduced, they can be easily incorporated into the existing hierarchy by:
1. Adding new subfolders (e.g., `animations` under molecules).
2. Creating new categories if necessary (e.g., `widgets` for custom interactive UI components).
