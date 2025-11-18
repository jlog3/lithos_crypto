# Lithos Crypto
Web app for exploring procedural rocks using cryptographic hashing for infinite, consistent generation.

##Overview
This project generates simulated 3D rock formations procedurally using SHA-256 hashing. Each point in an infinite 3D space is determined by hashing a seed combined with coordinates, producing a normalized value that selects minerals based on fixed probabilities. It's designed for abstract exploration, emphasizing cryptographic consistency—same inputs always yield the same outputs, enabling reproducible "worlds."
Stack:

- Backend: Python 3.10 with Flask for API, hashlib for hashing, NumPy for array ops.
- Frontend: React with React Three Fiber (@react-three/fiber, @react-three/drei) for 3D rendering using Three.js.
- Environment: Managed via Conda (environment.yaml) and pip (requirements.txt).
- Other: CORS for cross-origin requests, proxy setup in package.json for dev.

##Prerequisites

- [Miniconda or Anaconda](https://docs.conda.io/en/latest/miniconda.html) for Python environment management.
- Node.js (v14+) and npm for the frontend (install via https://nodejs.org/).

## Setup and Run
1. Clone the repo:
git clone https://github.com/jlog3/lithos_crypto.git
cd lithos_crypto


2. Run the startup script—it handles everything (creates/activates Conda env named lithos_explore, installs deps, starts servers):
```bash
./start.sh
```
- Backend (Flask) runs on http://localhost:5000.
- Frontend (React) runs on http://localhost:3000 (proxies API calls to backend).

3. Open http://localhost:3000 in your browser. Enter a seed, location (hashed to offsets), or manual offsets to explore 3D regions.

## Manual Setup (if needed)
- Create/activate Conda env: `conda env create -f environment.yaml && conda activate lithos_crypto`
- Backend: `cd backend && pip install -r requirements.txt && python app.py`
- Frontend (separate terminal): `cd frontend && npm install && npm start`

## Features
- Procedural 3D chunk generation with infinite exploration via offsets and seeds.
- Mineral distribution based on hash-normalized probabilities (e.g., 40% void, 30% quartz).
- Location input hashed to unique offsets for "region-specific" simulation.
- 3D visualization with orbit controls, instanced rendering for efficiency.
- Educational panel explaining hashing and probabilities.
- API endpoints: /api/mineral, /api/chunk3d, /api/slice2d, /api/offsets.
- Size/zoom controls with caps for performance.

## Notes
- This version focuses purely on cryptographic procedural generation—no real geologic data.
- For production, deploy backend with Gunicorn/NGINX and build frontend statically (npm run build).
- Optimize for large chunks: Consider caching or faster hashes if needed.
- If CORS issues: Already handled via flask-cors.
- To stop: Ctrl+C in the terminal running start.sh.
- Future ideas: Add more minerals, Perlin noise for vein patterns, export to OBJ.
