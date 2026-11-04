# Trello Clone Components

## Button

- **Variants**: primary, secondary, ghost, danger
- **Sizes**: sm (32px), md (40px), lg (48px)
- **States**: default, hover, active, focus-visible (2px ring, accent), disabled, loading
- **Tokens**: bg accent, text on-accent, radius md, font sm/600
- **Accessibility**: real `<button>`, visible focus, loading keeps the label for screen readers
- **Used On**: S02 (Board View), S07 (Booking Page), S09 (Details Form)

## TextField

- **Variants**: default, error, success
- **Sizes**: sm (32px), md (40px), lg (48px)
- **States**: default, hover, active, focus-visible, disabled, error, success
- **Tokens**: bg surface, text text, border border-input, radius md, font sm/400
- **Accessibility**: real `<input>`, visible focus, error/success states for screen readers
- **Used On**: S03 (Card View), S09 (Details Form)

## Modal

- **Variants**: default, danger
- **Sizes**: sm (320px), md (480px), lg (640px)
- **States**: default, open, closed
- **Tokens**: bg surface, text text, border border, radius lg, shadow lg
- **Accessibility**: real `<dialog>`, focus trap, close button, escape key
- **Used On**: S04 (Planner), S05 (Inbox)

## Card

- **Variants**: default, selected
- **Sizes**: sm (240px), md (320px), lg (400px)
- **States**: default, hover, active, selected
- **Tokens**: bg surface, text text, border border, radius md, shadow sm
- **Accessibility**: real `<div>`, hover/active states for screen readers
- **Used On**: S02 (Board View), S03 (Card View)
