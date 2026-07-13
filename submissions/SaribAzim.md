## Name
Sarib Azim

## Project and Role
voiceMonitor, Research Engineer

## Expected Contribution
As the Research Engineer on voiceMonitor, I would focus on the fatigue and vocal load estimation layer that sits on top of auralis vfs's streamed features, since that is where the largest gap between raw signal and usable insight exists. My background is in speech and time series machine learning, including a fine tuned Whisper model for Urdu automatic speech recognition, which gave me hands on experience with real time audio pipelines and the tradeoffs between latency and accuracy in streaming inference. I would start by profiling what auralis vfs actually outputs frame by frame, then design the fatigue and load scoring logic against real session recordings rather than assuming clean lab quality audio, since microphone input in real deployments is noisy and inconsistent.

## Question
Does fatigue level get computed as a running or cumulative score across the session, or as a point in time estimate recalculated on a rolling window? That affects whether the design needs session level state management or can stay stateless per chunk.