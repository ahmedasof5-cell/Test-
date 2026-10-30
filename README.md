# FaceBlend Studio — Beta 0.1

A browser-based, non-generative face replacement prototype for GitHub Pages. It uses MediaPipe Face Landmarker (468/478 facial landmarks) and 2D triangle texture warping. It does not synthesize unseen facial regions.

## Important prototype limitations

- This first build uses CDN-hosted MediaPipe JavaScript/WASM and downloads the official `face_landmarker.task` model at runtime. It does **not** yet bundle these binary dependencies locally. If the CDN or Google model host is blocked on the user's network, the tracker will not start.
- The current texture warp uses one still image as the texture source. It works best with a near-frontal reference and modest head movement. Profile turns, occlusion, hairline/ears, lighting mismatch and large expression changes can create visible seams or stretched areas.
- Export currently records the processed canvas video only; original audio is not muxed into the output. Browser support for `MediaRecorder` and MP4/WebM varies by iOS/Safari version.
- This is a technical MVP, not a TikTok-quality face swap. No claim of perfect realism or 3D reconstruction.

## Deploy to GitHub Pages from iPhone

1. In Safari, sign in to GitHub and create a **Public** repository named `faceblend-studio`.
2. Open the repository, choose **Add file → Upload files**.
3. Upload `index.html`, `app.js`, `style.css`, and `README.md` (keep them in the repository root).
4. Open **Settings → Pages**.
5. Under **Build and deployment**, choose **Deploy from a branch**, select `main` and `/ (root)`, then Save.
6. Wait for GitHub Pages to publish. Your site address will be `https://YOUR-USERNAME.github.io/faceblend-studio/`.
7. Open that address in Safari. Choose a short video and a clear reference image, then tap **Load face tracker**.

## Next engineering milestones

1. Bundle the MediaPipe WASM files and model under `/assets` so the app does not depend on runtime CDNs.
2. Add face oval masking, feathered edges, color transfer and exposure matching.
3. Add temporal landmark smoothing and confidence/occlusion handling.
4. Add audio-preserving export using a browser-compatible muxing pipeline, then test on actual iPhone hardware.
5. Improve side-view handling with multiple reference angles or a 3D textured head model (still non-generative).

## Privacy

The selected video and face image are processed in the browser. The MediaPipe library and model are fetched from their configured hosts. No application backend or upload endpoint is included in this prototype. Do not use another person's face without their permission; label synthetic/altered media clearly where appropriate.
