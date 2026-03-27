# HW5 - Implementation Prototypes (Port 5176)

This repository tracks only the latest **port 5176** implementation prototype experience.

## Stack

- Vite
- React
- TypeScript

## Run
Install the GitHub as a zip, open the folder and go to the folder from terminal via cd. Then:
```bash
npm install
npm run dev
```

Open: [http://localhost:5176](http://localhost:5176)

## App Entry

- [`index.html`](index.html) -> `src/main.5176.tsx`
- Main app: [`src/port5176/Port5176App.tsx`](src/port5176/Port5176App.tsx)
- Styles: [`src/port5176/port5176.css`](src/port5176/port5176.css)

## Requirement Surfaces in 5176

The app includes dedicated requirement surfaces for:

1. Hello world app  
2. Hello styles  
3. Role-based dashboards and case organization  
4. Case creation and manual declarant entry  
5. Multi-file upload and tab-based document viewing  
6. Manual evidence linking between declarant fields and PDF regions  
7. Send-file validation and controlled send with explanation flow  
8. Review matrix (field x document)  
9. Field inspection modal with linked PDF region preview  
10. Real-time comments, notifications, and role-based routing

## Notes

- Case-level data is persisted in `localStorage` for the 5176 workflow.

## Build

```bash
npm run build
npm run preview
```

## AI Usage Attribution

- Portions of this repository were developed with AI coding assistance (including code generation, refactoring suggestions, bug-fix drafts, and documentation edits).
- Team members reviewed, tested, and adjusted AI-assisted output before accepting changes.
- Final responsibility for implementation decisions, correctness, and submission content remains with the team.