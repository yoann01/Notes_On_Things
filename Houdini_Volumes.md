## 1. Types of volumes
### a) vdb
- sdf (signed distance field) - good for collisions etc
  - 0 on the surface
  - negative outside
  - positive inside - this seem to be a lie.... Looks like it's other way around...
  - it's opposite of native Houdini volumes
  - gradient direction points towards voxel with the smaller value
- fog - cheaper
- vdb from polygons can source v from points to vel volume (Vector type needs to be Velocity)
- can store vector fields
- almost always more memory eficient
- empty voxels inside and outside are not stored
### b) houdini volume (dense), e.g. iso offset
- fog
- sdf (Signed Distance Field)
  - each voxel stores value that means how close it is to the surface
  - surface = 0
  - inside - negative
  - outside - positive valueas
  - better results when using non intersecting geo - use boolean to remove intersecting geo
  - default mode of contruction - scan - can produce lines - artifacts - switch it off to avoid artifacts
### c) heighfield 
- is dense volume
## 2. VDB
- see vdb volumes fields/groups manipulation here: https://vimeo.com/272793390 at 46 min
- created by VDB from polygons- to create volume source for pyro sim
  - can add surface attributes as new volumes in the same VDB
  - point.v, VDB name vel
  - density is created by default
- blast can delete volume by group e.g. density
- use name sop to rename volume fields (groups)
- can use merge to merge back different fields/groups into one volume
## 3. Creating
- Iso offset - from polys
## 4. Visualizing
- Volume visualisation SOP
  - doesn't change anything, just changes how this looks in viewport
  - Density scale 10
## 5. Operations
- Volume mix
  - when changing "post multiply" you actually change the data stored int he voxels
## 6. Cloud and cloud noise SOPs
- vdb volume
- byaanimating time in advection pane in cloud noise sop you can make animated puff without simulation
- build low res then kick the res to 300
## 7. S. K. Vel volumes
### a) nodes
- Bound sop around your geo + some padding
- volume Sop named vel, vector
- volume vop with bind export vel 3 floats (vector)
- aaflow noise to create vectors (3d noise)
### b) preview
- volume slice from volume vop
- volume trail with left input from volume slice and right input from volumevop with noise bvelocities
  - switch off detect range - this ir remapping colors to range on every frame, so you will not know when things are speeding up.
## 8. VDB from particles
- if point radius scale is smaller than minimum radius in * voxel size then it will not mesh it
- to fix you can set the minimum radius to 0
- good results with radius = voxel soze, or voxel size smaller than radius
## 9. VDB to see camera frustrum
- vdb from camera
- extend z far if too short
## 10. VDB Advec Point
- can move points using volume vel
## 11. Make vel volume
- model
- vdb from poly
- plus in surface attributes
- attribute point v
- VDB name is vel
- Vector Type is displacement/velocity
## 12. Volume velocity sop
- has presets for noise and vortex
## 13. Volume vex
- @density = noise(@P)
## 14. Volume rasterize sop
- can create vel volume from N attribute
