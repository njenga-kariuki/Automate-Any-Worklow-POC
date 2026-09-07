# Video-to-Workflow Capture

A proof of concept that turns a narrated screen recording into an editable workflow diagram. It connects multimodal analysis with a structured representation of actions, inputs, outputs and decision points.

<div>
    <a href="https://www.loom.com/share/d8724535ef7c4da589168639d906facf">
      <p>Demo Video</p>
    </a>
    <a href="https://www.loom.com/share/d8724535ef7c4da589168639d906facf">
      <img style="max-width:300px;" src="https://cdn.loom.com/sessions/thumbnails/d8724535ef7c4da589168639d906facf-2c10e2ee62a0a3d9-full-play.gif">
    </a>
  </div>

## Project Context

Workflow automation tools like N8n and Zapier are powerful but have steep learning curves. This project explores whether AI can bridge that gap by letting users demonstrate workflows naturally through screen recordings.

The core idea: record yourself doing any computer task while explaining what you're doing, then get back a structured workflow diagram that captures both the visual actions and spoken context. The example workflow shows saving a daily cat picture from Google Images with specific preferences (always pick from the second row, save to a particular folder with today's date).

## Architecture Overview

The system processes recordings through a four-stage AI pipeline:

1. **Video Processing** - Extracts frames and audio from uploaded recordings
2. **Raw Extraction** - Gemini 2.0 Flash analyzes visual frames while Claude processes the combined visual/audio context into a chronological transcript
3. **Workflow Organization** - Claude structures the raw data into logical steps with inputs, outputs, and user considerations
4. **Block Generation** - Claude converts organized workflows into an interactive block-based diagram with different intents (edit, view, search, generate, etc.)

The frontend displays the resulting workflow as an editable React Flow diagram where users can modify connections, update block properties, and export the structure as JSON. Workflow execution is outside this implementation; the "Run Workflow" control demonstrates the proposed interaction.

## Technical Stack Implementation

**Frontend**: React with TypeScript, Tailwind CSS, React Flow for diagram visualization

**Backend**: Express.js with multimodal AI integrations

**AI Services**: 
- Google Gemini 2.0 Flash for video frame analysis
- Anthropic Claude 3.7 Sonnet for transcript generation, workflow organization, and block structure creation
- Google Cloud Speech-to-Text for audio transcription

**File Handling**: Google Cloud Storage with resumable uploads for large video files

**Video Processing**: FFmpeg for frame extraction and audio separation

The proof of concept demonstrates end-to-end processing from video upload through AI analysis to interactive workflow visualization, storing intermediate outputs for debugging and iteration.

## Project status and local setup

Built in April 2025. The recorded demo shows the capture-to-diagram pipeline. The source preserves the implementation and design documents; uploaded screen recordings and extracted frames are excluded.

For local exploration, install the dependencies with `npm ci`, install FFmpeg, and configure the process environment using [.env.example](.env.example). The pipeline requires Anthropic and Google AI credentials plus Google Cloud Storage and Speech-to-Text configuration. `npm run dev` starts the application. Runtime upload directories are created automatically.

Review model IDs, cloud permissions and dependency versions before connecting current services. The published source has not been revalidated end to end against today's APIs. The current visual analysis samples the beginning, middle and end of a recording, so longer or more detailed workflows need a denser capture strategy.
