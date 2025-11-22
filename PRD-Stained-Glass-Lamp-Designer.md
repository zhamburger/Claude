# Product Requirements Document: Stained Glass Lamp Designer

## 1. Product Overview

### 1.1 Product Name
**Stained Glass Lamp Designer - Professional Edition**

### 1.2 Product Description
A browser-based 3D design tool that allows users to create and customize professional stained glass lamp designs in real-time. The application provides an interactive 3D environment where users can experiment with different lamp shapes, colors, patterns, materials, and lighting configurations to design unique decorative lamps.

### 1.3 Target Audience
- Interior designers and decorators
- Artisans and craftspeople specializing in stained glass
- Home design enthusiasts
- Custom lamp manufacturers
- Students and educators in design programs
- Online retailers offering customizable home décor

### 1.4 Problem Statement
Traditional stained glass lamp design requires significant artistic skill, time, and physical materials for prototyping. There is no easy way for customers to visualize custom lamp designs before commissioning them, and designers lack accessible digital tools for rapid prototyping and client presentations.

### 1.5 Solution
A real-time 3D design tool that enables instant visualization of stained glass lamps with professional-quality rendering, allowing users to experiment with unlimited design variations at no material cost.

---

## 2. Product Goals & Success Metrics

### 2.1 Primary Goals
1. Enable users to design custom stained glass lamps without technical 3D modeling expertise
2. Provide photorealistic rendering that accurately represents final product appearance
3. Support rapid iteration and experimentation with design variations
4. Allow users to save and export their designs

### 2.2 Success Metrics
- User engagement: Average session duration > 5 minutes
- Design iteration: Average designs created per session > 3
- Export/save rate: > 40% of sessions result in saved designs
- User satisfaction: Net Promoter Score (NPS) > 50

---

## 3. Core Features & Specifications

### 3.1 3D Visualization Engine

#### 3.1.1 Technical Implementation
- **Rendering Engine**: Three.js (WebGL-based)
- **Graphics Quality**:
  - Anti-aliasing enabled
  - Shadow mapping (PCFSoftShadowMap)
  - Tone mapping (ACES Filmic)
  - Realistic glass material with transmission, reflection, and refraction
  - Metallic frame materials with proper PBR (Physically Based Rendering)

#### 3.1.2 Scene Components
- Lamp model with dynamic geometry
- Display platform (8-unit radius cylinder)
- Professional lighting setup (ambient, directional, internal point light)
- Dark gradient background for optimal visibility

### 3.2 Lamp Geometry Configuration

#### 3.2.1 Base Shapes
Six preset shapes with distinct geometric characteristics:

| Shape | Description | Default Segments |
|-------|-------------|------------------|
| Classic Dome | Rounded top, traditional Tiffany style | 16 |
| Cone | Tapered pyramid shape | 12 |
| Cylinder | Straight vertical walls | 8 |
| Hexagonal | Six-sided geometric design | 6 |
| Octagonal | Eight-sided traditional design | 8 |
| Square Pyramid | Four-sided mission style | 4 |

#### 3.2.2 Adjustable Parameters

**Segments Control**
- Range: 6-32 segments
- Default: 16
- Purpose: Controls panel count and geometric complexity
- Impact: More segments = smoother curves, more intricate patterns

**Height Control**
- Range: 3.0-8.0 units
- Default: 5.0
- Step: 0.5
- Purpose: Vertical dimension of lamp shade

**Radius Control**
- Range: 2.0-6.0 units
- Default: 4.0
- Step: 0.5
- Purpose: Horizontal width of lamp shade

#### 3.2.3 Structural Components
- **Base**: Cylindrical with gradient taper (1.5-2.0 unit radius, 1 unit height)
- **Stem**: Connecting column (0.3-0.5 unit radius, 2 units height)
- **Shade**: Main glass panel structure (configurable geometry)
- **Frame**: Top/bottom rings and vertical separators
- **Cap**: Decorative top piece (cone geometry)

### 3.3 Color & Pattern System

#### 3.3.1 Color Configuration
**Primary, Secondary, and Accent Colors**
- Three-color palette system
- Full RGB color picker for each
- Default colors:
  - Primary: #ff6b6b (coral red)
  - Secondary: #4ecdc4 (turquoise)
  - Accent: #ffe66d (golden yellow)

**Quick Color Swatches**
12 pre-defined colors in grid layout for rapid selection:
- Coral, turquoise, yellow, sky blue, cream, crimson
- Navy, mint, peach, rose, pink, purple

#### 3.3.2 Pattern Options
Six algorithmic pattern generators:

| Pattern | Algorithm | Visual Effect |
|---------|-----------|---------------|
| Alternating | Sequential color cycling (i % 3) | Regular repeating pattern |
| Gradient | Position-based distribution | Smooth color transitions |
| Random | Random color assignment | Unpredictable, artistic look |
| Striped | Paired segment coloring | Bold horizontal bands |
| Spiral | Progressive offset pattern | Rotating color flow |
| Checker | Position-based alternation | Checkerboard-like effect |

### 3.4 Glass Material Properties

#### 3.4.1 Physical Properties
**Opacity Control**
- Range: 0.3-1.0
- Default: 0.8
- Purpose: Controls transparency of glass
- Visual impact: Lower = more see-through

**Translucency (Transmission)**
- Range: 0.0-1.0
- Default: 0.7
- Purpose: Light transmission through glass
- Technical: Three.js transmission property
- Impact: Affects light refraction and glow

#### 3.4.2 Glass Textures
Four texture variants (future enhancement):
- Smooth (default): Clear, polished glass
- Rippled: Wavy surface texture
- Frosted: Diffused, matte appearance
- Cathedral: Traditional textured glass

#### 3.4.3 Material Rendering
**MeshPhysicalMaterial Properties**:
- Roughness: 0.05 (highly polished)
- Metalness: 0
- Transmission: User-controlled
- IOR (Index of Refraction): 1.5 (realistic glass)
- Clearcoat: 1.0 (glossy surface)
- Clearcoat Roughness: 0.05
- Reflectivity: 0.9
- Side: DoubleSide (visible from all angles)

### 3.5 Lighting System

#### 3.5.1 Internal Lamp Light
**Point Light Configuration**
- Type: THREE.PointLight
- Position: Center of shade (y = 3 + height/2)
- Default intensity: 2.0
- Range: 20 units
- Color: Warm white (#fff5e6)
- Shadow casting: Disabled (performance optimization)

**Adjustable Parameters**:
- Intensity: 0.5-4.0 (slider control)
- Color: Full RGB color picker
- Default: Warm incandescent tone

**Glow Visualization**
- Sphere geometry (0.3 unit radius)
- Emissive material
- Opacity: 0.8
- Represents visible bulb

#### 3.5.2 Scene Lighting
**Ambient Light**
- Intensity: 0.4 (default) or 0.1 (when disabled)
- Color: White (0xffffff)
- Toggle control available

**Directional Lights**
- Main light: Position (10, 10, 10), intensity 0.8, shadow casting enabled
- Fill light: Position (-10, 5, -10), intensity 0.3, blue tint (0x6688ff)
- Shadow map resolution: 2048x2048

### 3.6 Frame & Base Materials

#### 3.6.1 Material Options
Five metallic finishes with realistic PBR properties:

| Material | Color (Hex) | Roughness | Metalness | Visual Description |
|----------|-------------|-----------|-----------|-------------------|
| Antique Bronze | 0x8b6914 | 0.4 | 0.8 | Warm, aged appearance |
| Polished Brass | 0xb5a642 | 0.3 | 0.9 | Bright, golden shine |
| Copper | 0xb87333 | 0.4 | 0.8 | Reddish-brown metal |
| Black Iron | 0x1a1a1a | 0.6 | 0.5 | Dark, matte finish |
| Silver | 0xc0c0c0 | 0.2 | 0.95 | Bright, reflective |

#### 3.6.2 Frame Components
**Top and Bottom Rings**
- Geometry: Torus
- Radius matches shade dimensions
- Thickness: User-controlled (0.05-0.2 units)
- Default thickness: 0.1

**Structural Elements**
- Base and stem use selected material
- Shadow casting enabled for realism
- Consistent material across all frame components

### 3.7 Design Presets

#### 3.7.1 Professional Style Presets
Eight historically-inspired design templates:

**1. Tiffany Classic**
- Shape: Dome
- Colors: Coral (#ff6b6b), Turquoise (#4ecdc4), Yellow (#ffe66d)
- Pattern: Alternating
- Frame: Bronze
- Segments: 12
- Style: Traditional American art glass

**2. Victorian**
- Shape: Dome
- Colors: Brown (#8b4513), Purple (#9b59b6), Gold (#ffd700)
- Pattern: Gradient
- Frame: Brass
- Segments: 16
- Style: Ornate 19th century design

**3. Modern Geometric**
- Shape: Cylinder
- Colors: Blue (#3498db), Green (#2ecc71), Orange (#f39c12)
- Pattern: Striped
- Frame: Black
- Segments: 8
- Style: Contemporary minimalist

**4. Art Deco**
- Shape: Cone
- Colors: Red (#e74c3c), Teal (#1abc9c), Yellow (#f1c40f)
- Pattern: Checker
- Frame: Silver
- Segments: 12
- Style: 1920s-1930s glamour

**5. Prairie School**
- Shape: Square
- Colors: Tan (#d4a574), Green (#8fbc8f), Gold (#daa520)
- Pattern: Striped
- Frame: Brass
- Segments: 4
- Opacity: 0.7
- Style: Frank Lloyd Wright inspired

**6. Mediterranean**
- Shape: Dome
- Colors: Blue (#1e90ff), Gold (#ffd700), White (#ffffff)
- Pattern: Spiral
- Frame: Gold
- Segments: 20
- Style: Coastal European design

**7. Gothic Cathedral**
- Shape: Hexagon
- Colors: Indigo (#4b0082), Dark Red (#8b0000), Navy (#191970)
- Pattern: Alternating
- Frame: Black
- Segments: 6
- Opacity: 0.75
- Translucency: 0.3
- Style: Medieval church windows

**8. Mission Style**
- Shape: Octagon
- Colors: Peru (#cd853f), Saddle Brown (#8b4513), Burlywood (#deb887)
- Pattern: Gradient
- Frame: Bronze
- Segments: 8
- Opacity: 0.65
- Style: Arts and Crafts movement

### 3.8 Interactive 3D Controls

#### 3.8.1 Camera Control System
**Mouse Interactions**:

| Action | Control | Function |
|--------|---------|----------|
| Rotate | Left Click + Drag | Orbit camera around lamp |
| Pan | Right Click + Drag | Move camera target position |
| Zoom | Mouse Scroll Wheel | Adjust camera distance |
| Reset View | Double Click | Return to default position |

**Camera Constraints**:
- Distance range: 8-30 units
- Default distance: 15 units
- Vertical rotation: -90° to +90° (prevents flipping)
- Default position: (0, 8, 15)
- Target: (0, 4, 0)

#### 3.8.2 Camera Behavior
- Smooth interpolation using lerp
- Context menu disabled on canvas
- Real-time response to input
- Maintains aspect ratio on window resize

### 3.9 Design Management

#### 3.9.1 Save Design Function
**Export Format**: JSON
**Exported Data**:
```json
{
  "shape": "dome",
  "segments": 16,
  "height": 5,
  "radius": 4,
  "primaryColor": 16738411,
  "secondaryColor": 5164484,
  "accentColor": 16770669,
  "opacity": 0.8,
  "translucency": 0.7,
  "pattern": "alternating",
  "glassTexture": "smooth",
  "lightIntensity": 2,
  "lightColor": 16774630,
  "frameMaterial": "bronze",
  "frameThickness": 0.1
}
```

**File Output**:
- Filename: `stained-glass-lamp-design.json`
- Download trigger: Automatic browser download
- User feedback: Alert confirmation

#### 3.9.2 Randomize Function
**Randomization Scope**:
- Shape: Random from 6 options
- Segments: Random 6-32
- Colors: Random RGB values (all three)
- Pattern: Random from 6 options
- Frame material: Random from 5 options
- UI automatically updates to reflect changes

#### 3.9.3 Reset Function
Restores all parameters to default values:
- Shape: Dome
- Segments: 16
- Height: 5.0
- Radius: 4.0
- Colors: Default coral/turquoise/yellow palette
- Pattern: Alternating
- Frame: Bronze, 0.1 thickness
- Updates UI controls to match

---

## 4. User Interface Design

### 4.1 Layout Structure

#### 4.1.1 Canvas Container
- Full viewport coverage (100vw × 100vh)
- 3D rendering surface
- Background: Dark gradient (#2c3e50 to #3498db)

#### 4.1.2 UI Control Panel
**Position**: Absolute, top-right
**Dimensions**: 350px width, max-height 95vh
**Styling**:
- White background (95% opacity)
- 15px border radius
- Backdrop blur effect
- Scrollable content
- Drop shadow for depth

**Header**:
- Title: "🎨 Stained Glass Designer"
- 24px font size
- Orange underline accent (#e67e22)

#### 4.1.3 Info Panel
**Position**: Absolute, bottom-left
**Content**: Control instructions
- Left Click + Drag: Rotate lamp
- Right Click + Drag: Pan view
- Scroll: Zoom in/out
- Double Click: Reset view

**Styling**:
- White background (90% opacity)
- Backdrop blur
- Rounded corners
- 13px font

### 4.2 Control Organization

#### 4.2.1 Section Structure
Controls grouped into logical sections:
1. Lamp Style (Presets)
2. Lamp Shape
3. Glass Colors
4. Glass Properties
5. Pattern Design
6. Lighting
7. Frame & Base
8. Action Buttons

#### 4.2.2 Control Types

**Preset Buttons**
- 2-column grid layout
- Gradient blue background
- Hover effect: Scale transform

**Range Sliders**
- Full-width input
- Real-time value display
- Labeled with current value
- Smooth response

**Color Pickers**
- Native HTML5 color input
- 40px height for easy interaction
- Immediate visual feedback

**Dropdowns**
- Full-width select elements
- Styled borders
- Consistent padding

**Pattern Buttons**
- 3-column grid
- Active state highlighting
- Bordered design

**Toggle Switch**
- Custom-styled checkbox
- Animated slider transition
- Orange active state

### 4.3 Visual Design System

#### 4.3.1 Color Palette
**Primary Brand Colors**:
- Primary Orange: #e67e22
- Dark Orange: #d35400
- Dark Blue: #2c3e50
- Medium Blue: #34495e

**UI Colors**:
- White: #ffffff
- Light Gray: #ecf0f1
- Border Gray: #ddd
- Text Gray: #555

#### 4.3.2 Typography
- Font Family: Georgia, serif (elegant, traditional)
- H1: 24px
- H3: 16px
- Labels: 13px
- Body: 13-14px

#### 4.3.3 Interactive Feedback
- Hover effects on all buttons
- Transform animations (scale, translateY)
- Selected state indicators
- Real-time value updates
- Shadow effects on hover

---

## 5. Technical Architecture

### 5.1 Technology Stack
- **Frontend Framework**: Vanilla JavaScript
- **3D Engine**: Three.js r128
- **Rendering**: WebGL
- **File Format**: HTML5 (standalone single file)
- **Browser APIs**: Canvas, File Download API

### 5.2 Performance Considerations

#### 5.2.1 Optimization Strategies
- Shadow map resolution: 2048×2048 (balanced quality/performance)
- Soft shadow algorithm (PCF)
- Geometry caching (recreate only on parameter change)
- No unnecessary animations
- Efficient event listeners
- RequestAnimationFrame for rendering loop

#### 5.2.2 Resource Management
- Single geometry instances per component
- Material reuse where possible
- Proper cleanup on lamp recreation
- Responsive resize handling

### 5.3 Browser Compatibility
**Minimum Requirements**:
- WebGL support
- ES6 JavaScript
- HTML5 Canvas
- Modern browser (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

### 5.4 Code Organization

#### 5.4.1 Global Variables
- `scene`, `camera`, `renderer`: Three.js core
- `lampConfig`: Central configuration object
- `lamp`: Main lamp group
- `glassSegments`, `frameSegments`: Component arrays
- `internalLight`: Point light reference
- Camera control variables

#### 5.4.2 Function Categories
**Creation Functions**:
- `createLamp()`: Main lamp builder
- `createShade()`: Glass panel generation
- Geometric primitive creators

**Update Functions**:
- `updateLampShape()`, `updateSegments()`, etc.
- `updateColors()`, `updateGlassProperties()`
- `updateLighting()`, `updateFrame()`
- `updateCamera()`, `updateUIFromConfig()`

**Utility Functions**:
- `loadPreset()`: Apply style presets
- `randomizeDesign()`: Random generation
- `saveDesign()`: JSON export
- `resetToDefault()`: Reset state

**Animation**:
- `animate()`: Main render loop
- Window resize handler

---

## 6. User Experience Flow

### 6.1 Initial Load Experience
1. Page loads with default Tiffany-style lamp
2. Camera positioned for optimal view
3. UI panel visible with all controls
4. Info panel shows control instructions
5. Lamp fully rendered and interactive

### 6.2 Design Creation Workflow

#### 6.2.1 Preset-Based Start
1. User clicks style preset button
2. Lamp instantly transforms
3. UI controls update to match preset
4. User explores preset with camera controls
5. User fine-tunes parameters

#### 6.2.2 Custom Design Workflow
1. User selects base shape
2. Adjusts geometry (segments, height, radius)
3. Chooses color palette
4. Selects pattern
5. Configures glass properties
6. Adjusts lighting
7. Selects frame material
8. Saves or randomizes

#### 6.2.3 Exploration Mode
1. User uses randomize function
2. Reviews generated design
3. Keeps elements they like
4. Manually adjusts others
5. Iterates until satisfied
6. Saves final design

### 6.3 Interaction Patterns

#### 6.3.1 Real-Time Updates
All controls provide instant visual feedback:
- Sliders: Update while dragging
- Color pickers: Change on color selection
- Dropdowns: Change on option select
- Buttons: Immediate transformation

#### 6.3.2 Visual Feedback Mechanisms
- Value displays update in real-time
- Selected states clearly indicated
- Hover effects on interactive elements
- 3D view updates immediately
- Save confirmation alert

---

## 7. Future Enhancements

### 7.1 Phase 2 Features

#### 7.1.1 Advanced Customization
- Custom panel shapes (beyond geometric primitives)
- Individual panel color assignment
- Texture mapping for glass patterns
- Custom logo/image integration
- Multiple internal lights

#### 7.1.2 Enhanced Materials
- Iridescent glass effects
- Beveled glass edges
- Jewel accents
- Aged patina effects on frames
- Crystal elements

#### 7.1.3 Design Management
- Design library (save multiple designs)
- Load saved designs
- Design sharing (URL parameters)
- Gallery of community designs
- Design history/undo

### 7.2 Phase 3 Features

#### 7.2.1 Export Options
- High-resolution render export (PNG/JPG)
- 3D model export (OBJ, GLTF)
- Technical drawings (SVG)
- Material specifications (PDF)
- Cost estimation

#### 7.2.2 Collaboration
- User accounts
- Shared design projects
- Comments and annotations
- Design versioning
- Manufacturer integration

#### 7.2.3 Advanced Visualization
- Room context preview
- Different lighting scenarios (day/night)
- Size comparison tools
- AR preview (mobile)
- Multiple lamp compositions

### 7.3 Technical Improvements
- WebGL 2.0 support
- Progressive Web App (PWA)
- Offline functionality
- Touch gesture controls
- Performance profiling
- Accessibility improvements (keyboard navigation)

---

## 8. Success Criteria & KPIs

### 8.1 User Engagement Metrics
- **Average Session Duration**: Target > 5 minutes
- **Designs Created per Session**: Target > 3
- **Return User Rate**: Target > 30% within 30 days
- **Tool Interaction Rate**: > 80% of users adjust 3+ parameters

### 8.2 Business Metrics
- **Save/Export Rate**: > 40% of sessions
- **Preset Usage**: Each preset used in > 10% of sessions
- **Randomize Feature Usage**: > 25% of users
- **Mobile vs Desktop**: Track usage patterns

### 8.3 Technical Performance
- **Initial Load Time**: < 3 seconds
- **Frame Rate**: Maintain 60 FPS during interaction
- **Browser Compatibility**: 95%+ of modern browsers
- **Error Rate**: < 0.1% of sessions

### 8.4 Quality Metrics
- **User Satisfaction**: NPS > 50
- **Design Quality**: User-rated visual realism > 4/5
- **Ease of Use**: SUS (System Usability Scale) > 70
- **Bug Reports**: < 5 critical bugs per month

---

## 9. Constraints & Assumptions

### 9.1 Technical Constraints
- Browser must support WebGL
- Single-page application (no backend)
- No user authentication system
- Designs stored locally only (no cloud sync)
- Limited to Three.js r128 capabilities

### 9.2 Design Constraints
- Lamp geometry limited to radial symmetry
- Frame must be consistent material throughout
- Internal light is single point source
- Pattern algorithms are pre-defined (not custom)

### 9.3 Assumptions
- Users have basic understanding of lamp components
- Users can use mouse/trackpad effectively
- Modern browser with adequate GPU
- Screen resolution minimum 1280×720
- Users interested in decorative lighting design

### 9.4 Out of Scope (v1.0)
- User accounts and authentication
- Backend server integration
- Multi-user collaboration
- Payment processing
- Manufacturer ordering integration
- Mobile app version
- Custom pattern creation tool
- Animation of lamp (rotating display)

---

## 10. Appendix

### 10.1 Glossary

**Terms**:
- **Shade**: The glass portion of the lamp that covers the light source
- **Segments**: Individual glass panels that make up the shade
- **Frame**: Metal structure holding glass panels together
- **Base**: Bottom support structure of lamp
- **Stem**: Vertical connector between base and shade
- **Translucency**: Amount of light passing through glass
- **IOR**: Index of Refraction - how light bends through material
- **PBR**: Physically Based Rendering - realistic material representation

### 10.2 References
- Three.js Documentation: https://threejs.org/docs/
- Tiffany Lamp History: Historical design reference
- WebGL Specification: Technical rendering standards
- Color Theory: Design palette creation
- Material Science: Glass and metal properties

### 10.3 Version History
- **v1.0** (Current): Initial release with core features
- Professional rendering quality
- 8 preset styles
- Full customization controls
- JSON export capability

### 10.4 Contact & Support
- Technical issues: [GitHub issues or support contact]
- Feature requests: [Product feedback channel]
- Design showcase: [Community gallery]

---

**Document Version**: 1.0
**Last Updated**: 2025-11-22
**Status**: Active Development
**Owner**: Product Team
