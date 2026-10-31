# ATOMVERSE 3.0 — Complete Chemistry Mass Lab

4 interactive laboratories in one React/TypeScript/Vite + React Three Fiber web application. **Development build, not classroom-certified**: scientific unit tests were run, but npm dependency installation/build and browser interaction could not be verified in the authoring environment.

## What's inside

- **LAB 01 Atom Forge** — inherited ATOMVERSE 2.0. Adjust p+/n0/e−, drag desktop particles to the canvas, side-by-side A/B and five short missions.
- **LAB 02 Mass Chamber** — 3D *analogical* balance, select isotope and number of atoms (or 1-u reference units), convert u to grams, compare quantities and show equation. This is NOT a physical atomic balance.
- **LAB 03 Isotope Reactor** — 3D representative particle mixture; dynamically weighted average of Cl-35 and Cl-37, 0–100% slider, A/B snapshot and concept check. These percentages are *user-chosen hypothetical compositions*, not natural abundance measurements.
- **LAB 04 Molecule Studio** — guided assembly of eight predefined molecules (not arbitrary valence bond creation), progress visible on 3D sphere/bond model, composition validation, relative molecular mass calculation and comparison. Incomplete assemblies are not chemically stable structures.

## Installation / verify

Requirements: Node.js 22 or a currently supported LTS. Install Node/npm on your own machine or use GitHub Actions.

```bash
npm install
npm test
npm run build
npm run dev
```

Use the Vite local URL printed by the terminal (usually http://localhost:5173/). Please check all four laboratory interactions and mobile screens before distributing to students. `npm run build` produces the `dist` folder.

## Update the existing GitHub repository (supaksiri/atomverse-2.0)

1. Back up the current repository (e.g. download ZIP or create a branch).
2. In the `atomverse-2.0` repository, upload or replace the CONTENTS of `ATOMVERSE_3_COMPLETE/` at the root — importantly, `package.json`, `index.html`, `src`, `tests`, `.github`, `vite.config.ts` and `tsconfig.json`.
3. Ensure the latest `.github/workflows/deploy.yml` exists, and Settings → Pages → Source is **GitHub Actions**.
4. In the Actions tab, open the deployment and confirm both npm tests AND build succeed, then visit https://supaksiri.github.io/atomverse-2.0/.
5. If deployment fails, read the build log and fix reported errors instead of deleting the repository. Do not upload `node_modules`.

Alternatively use a NEW repository named `atomverse-3.0` to preserve the previous release. The relative Vite `base: './'` is compatible with GitHub project pages.

**Important:** GitHub upload via browser of directories that already exist may require uploading files inside each directory, preserving paths. Git CLI or GitHub Desktop is more reliable for a whole-project update.

## Science / limitation notes

- The 3D scale is conceptual and not an experiment that physically measures an atom. The design uses absolute u for count-weighted samples and clearly identifies reference units.
- Chlorine isotope masses in `src/chemistry/mass.ts` are approximate published nuclide masses; abundance is deliberately interactive/hypothetical. The definition of 1 u uses C-12, and u-to-g uses 1.66053906660 × 10^-24 g.
- Relative molecular mass Mr is dimensionless. Standard classroom atomic weights are used for molecular formulas; values differ from exact isotopologue masses.
- 3D nuclear depiction and molecule geometry are simplified educational illustrations; electrons are not planetary trajectories.
- The 3D mass balance depicts equal-distance pans with angle controlled by relative difference; it is a *visual analogy*, not an instrument engineering simulation.
- The interactive particle reactor displays 80 representative spheres with composition rounded to integer counts (displayed percentage is exact from the slider).
- Four laboratories are available from the landing page. Classroom UX/accessibility and graphics performance have NOT been validated on actual student devices.

## Test status

Run `npm test` for deterministic scientific unit checks. Consult `TEST_REPORT.md` for executed checks and missing build/browser checks.
