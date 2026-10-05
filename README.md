# AD Attack Path Visualizer

An interactive, force-directed graph that visualizes Active Directory
relationships (users, groups, computers) and traces the shortest attack
path from any selected principal to Domain Admin — the same concept
BloodHound popularized, built from scratch with D3.js to understand the
graph-traversal logic underneath it.

## How it works
- `sample_data.json` models a small AD environment as nodes (User / Group /
  Computer) and edges (`MemberOf`, `AdminTo`, `HasSession`, `DCSync`) —
  the same primitives BloodHound collects via SharpHound.
- Click any node: the app runs a breadth-first search over the graph to
  find the shortest route to the Domain Admin target, then highlights that
  path and dims everything else.
- Drag nodes to rearrange, scroll to zoom.

## Run it
No build step — it's a static page.
```bash
cd ad-path-visualizer
python3 -m http.server 8000
# open http://localhost:8000
```

## Using it with real data
Replace `sample_data.json` with your own export shaped the same way. If
you're working from actual BloodHound JSON exports, add a small transform
script to map its `Nodes`/`Edges` format into this schema.

## Roadmap
- [ ] Import real BloodHound JSON exports directly (no manual transform)
- [ ] Highlight *all* paths to DA, not just the shortest
- [ ] Filter by edge type (e.g. show only Kerberoastable paths)
- [ ] Export the highlighted path as a Markdown attack narrative

## Disclaimer
Sample data only, representing a fictional home-lab domain (`lab.local`).
Use only against environments you own or are authorized to assess.
