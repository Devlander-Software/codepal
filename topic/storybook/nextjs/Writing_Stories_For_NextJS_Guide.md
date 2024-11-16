
# Writing Components and Storybook Files for a Project

## Overview

This guide provides a step-by-step approach to writing reusable components and corresponding Storybook files for **Next.js**, **Material UI**, and **Storybook**. It emphasizes best practices, including how to handle props, write reusable stories, and ensure your components work seamlessly in various environments.

---

## Why This Guide?

Many developers struggle with:
1. **Creating reusable components**: Ensuring components are flexible and customizable.
2. **Writing effective stories**: Covering all use cases and making stories interactive.
3. **Avoiding deployment issues**: Handling assets (like images) safely to prevent breaking in hosted environments (e.g., Netlify).

This guide will help you:
- Write clean, reusable components.
- Create robust Storybook stories that document all possible use cases.
- Use placeholders **only in Storybook files**, not the component itself, to ensure flexibility.

---

## Table of Contents

1. [Component Writing Guidelines](#component-writing-guidelines)
2. [Storybook File Writing Guidelines](#storybook-file-writing-guidelines)
3. [Best Practices](#best-practices)
4. [Example: AvatarBadge Component](#example-avatarbadge-component)
   - [Component File](#component-file)
   - [Stories File](#stories-file)
5. [Common Mistakes](#common-mistakes)

---

## Component Writing Guidelines

When writing a component, follow these principles:

1. **Keep the component flexible**:
   - Allow props to control all customizable features (e.g., styles, content).
   - Avoid hardcoding values inside the component (e.g., placeholder images).

2. **Use TypeScript for type safety**:
   - Define an `interface` or `type` for the component props.
   - Use optional props where necessary.

3. **Separate concerns**:
   - Do not include fallback content or default behavior that belongs in a story or parent component.

---

## Storybook File Writing Guidelines

When writing a Storybook file:
1. **Organize stories**:
   - Use a consistent folder structure and naming convention.
   - Example: `src/components/atoms/images/AvatarBadge.stories.tsx`.

2. **Use dynamic props**:
   - Define `args` for each story to demonstrate how props can be customized.

3. **Use placeholders safely**:
   - Use placeholder images or fallback values **only in the Storybook file** to demonstrate edge cases.

4. **Write multiple stories**:
   - Cover default states, interactive features, and error handling.

5. **Add documentation**:
   - Explain the purpose of each story.

---

## Best Practices

- **Keep the component agnostic**: Don’t assume a default image or content within the component.
- **Write stories for all use cases**:
   - Default state.
   - Custom props (e.g., different sizes or colors).
   - Edge cases (e.g., missing image source or text overflow).
- **Ensure components are reusable**: Components should be portable without requiring specific assets or dependencies.

---

## Example: AvatarBadge Component

### Component File

#### File: `AvatarBadge.tsx`

```typescript
import { Avatar, Badge } from '@mui/material';

/**
 * Props for the AvatarBadge component.
 * - `src`: The URL of the avatar image (required for flexibility).
 * - `alt`: The alternative text for the image.
 * - `badgeContent`: Optional content for the badge (e.g., numbers, icons).
 */
interface AvatarBadgeProps {
  src: string; // Component requires src to be passed
  alt: string; // Provides alternative text for accessibility
  badgeContent?: React.ReactNode; // Badge content is optional
}

/**
 * AvatarBadge Component
 * - Combines Material UI's Avatar and Badge components.
 * - Does not include a fallback image (fallbacks should be handled by parent components or stories).
 */
const AvatarBadge: React.FC<AvatarBadgeProps> = ({ src, alt, badgeContent }) => {
  return (
    <Badge badgeContent={badgeContent} color="secondary">
      <Avatar src={src} alt={alt} />
    </Badge>
  );
};

export default AvatarBadge;
```

### Explanation

- **No hardcoded values**: 
  - The component does not include a default `src` or `alt`.
  - This makes the component reusable and agnostic of specific assets.
- **Optional `badgeContent`**: 
  - Allows flexibility for use cases without badges.

---

### Stories File

#### File: `AvatarBadge.stories.tsx`

```typescript
import type { Meta, StoryObj } from '@storybook/react';
import AvatarBadge from './AvatarBadge';

/**
 * Meta configuration for AvatarBadge stories.
 * - Organizes stories under `components/atoms/images`.
 * - Ensures layout consistency by centering the component in Storybook.
 */
const meta: Meta = {
  title: 'components/atoms/images/AvatarBadge',
  component: AvatarBadge,
  parameters: {
    layout: 'centered',
  },
};

export default meta;

type Story = StoryObj;

/**
 * Default story for AvatarBadge.
 * - Uses a placeholder image to demonstrate the component.
 */
export const Default: Story = {
  args: {
    src: 'https://via.placeholder.com/150', // Placeholder for demo purposes
    alt: 'Default Avatar',
  },
};

/**
 * Story with badge content.
 * - Demonstrates the use of the badgeContent prop for notifications.
 */
export const WithBadge: Story = {
  args: {
    src: 'https://via.placeholder.com/150', // Placeholder for demo purposes
    alt: 'Avatar with Badge',
    badgeContent: 4,
  },
};

/**
 * Story for missing image source.
 * - Simulates a scenario where the `src` prop is not provided.
 * - Placeholder is used here to represent fallback behavior.
 */
export const MissingImage: Story = {
  args: {
    src: 'https://via.placeholder.com/150', // Simulate missing image in a story
    alt: 'Fallback Avatar',
    badgeContent: '!',
  },
};
```

### Explanation

- **Placeholders in Storybook only**:
  - The placeholder URL (`https://via.placeholder.com/150`) is used in the stories to simulate missing or dynamic image sources.
  - This keeps the component clean while demonstrating edge cases in Storybook.
- **Args for reusability**:
  - Props are passed via `args` to make stories interactive and maintainable.

---

## Common Mistakes

1. **Hardcoding fallbacks in the component**:
   - Avoid adding defaults like placeholder images in the component itself. Let the parent or Storybook handle fallbacks.

2. **Not covering edge cases**:
   - Always write stories for missing props, invalid data, and extreme scenarios.

3. **Forgetting documentation**:
   - Add TSDoc comments for props and stories to ensure clarity for other developers.

