# Neocortex AI Integration

## Overview
Simple Neocortex integration for creating AI-powered nodes on your canvas.

## What's Integrated

### 1. Neocortex API Service (`src/lib/neocortex.ts`)
- API key: `sk_f4b0fda4-4772-41ba-8b92-edf59d6e38f6`
- Project ID: `cmh5uhb1l0003jj04tahgqbm8`
- Base URL: `https://api.neocortex.link/v1`

### 2. AI Agent Button
Located in the **Node Canvas** (top-left toolbar)

**Features:**
- ✨ Sparkles icon with purple accent
- Fetches agents from your Neocortex project
- Creates nodes automatically on the canvas
- Shows loading state while fetching

## How to Test

### Step 1: Load a Robot
1. Click **"Upload Simulation"** in the sidebar
2. Upload your robot URDF ZIP file
3. Wait for the robot to load (you should see joints available)

### Step 2: Use AI Agent Button
1. Look for the **"AI Agent"** button in the top-left toolbar (next to Joint/Transition buttons)
2. Click the button
3. The system will:
   - Try to fetch agents from Neocortex
   - If no agents exist: Create a demo AI node with random joint values
   - If agents exist: Create nodes for each agent

### What Happens
- **Demo Mode**: If no agents in Neocortex, creates a node with randomized joint positions
- **Agent Mode**: Creates a node for each Neocortex agent with zero positions
- Nodes can be connected and animated just like regular Joint nodes
- All standard functionality works (dragging, connecting, animating, recording, exporting)

## API Endpoints Used

```typescript
// Get agents from your project
GET /v1/projects/{projectId}/agents

// Get project info
GET /v1/projects/{projectId}

// Query/Chat (future use)
POST /v1/projects/{projectId}/query
```

## Expected Behavior

### Success Cases:
1. **No agents found**: 
   - Toast: "No agents found. Creating demo AI node..."
   - Creates 1 AI-powered node with random pose
   - Toast: "Created AI-powered demo node!"

2. **Agents found**:
   - Creates nodes for each agent
   - Positions them horizontally (200px apart)
   - Toast: "Added X Neocortex agent(s)!"

### Error Cases:
1. **API Error**: 
   - Toast: "Failed to connect to Neocortex. Check console for details."
   - Check browser console for detailed error

2. **No Robot Loaded**:
   - Button is disabled
   - Upload a robot first

## Testing the API

To verify the Neocortex API is working, open browser console and run:

```javascript
// Test the API connection
fetch('https://api.neocortex.link/v1/projects/cmh5uhb1l0003jj04tahgqbm8/agents', {
  headers: {
    'Authorization': 'Bearer sk_f4b0fda4-4772-41ba-8b92-edf59d6e38f6',
    'Content-Type': 'application/json'
  }
})
.then(r => r.json())
.then(d => console.log('Neocortex Response:', d))
.catch(e => console.error('Error:', e));
```

## Future Enhancements

This is the **minimal viable integration**. Easy additions:
1. **AI-Generated Poses**: Query Neocortex to generate optimal joint configurations
2. **Smart Transitions**: AI-powered smooth motion planning
3. **Natural Language Control**: "Move arm to home position"
4. **Behavior Trees**: Create complex robot behaviors via Neocortex agents
5. **Real-time Adaptation**: Agents that adjust movements based on environment

## Files Modified
- `src/lib/neocortex.ts` - New API service
- `src/components/NodeGraph.tsx` - Added AI Agent button and logic

## Dependencies
No new dependencies required! Uses native `fetch` API.

