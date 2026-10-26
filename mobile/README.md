# KEYO Studio portable alpha

Runs KEYO's own JavaScript CPU engine in a dedicated worker. Not ONNX, Transformers.js, llama.cpp or a cloud API.

Node >=22.12: npm install, npm run build. For Android: install JDK 21 and Android SDK 36, run npm run android, then cd android && ./gradlew assembleDebug (Windows: gradlew.bat).

Debug APKs are test builds, not Play Store releases. Device execution and signing/release certification are separate from an APK compiling.

Models are not bundled. Explicitly accept each model licence, then download or import the exact pinned files (listed in ../src/portable-catalog.mjs). OPFS stores weights, IndexedDB stores chats. Both are local, not encrypted, and may be cleared by the browser/OS. Request storage persistence and keep your original model files.

CPU-only: F32/F16/BF16, 512 context tokens, at most 128 output tokens, bounded 256 KiB weight scratch space. No GPU, WASM/SIMD or integer quantization is shipped. Qwen2.5 0.5B and SmolLM2 135M have separate numerical evidence; this does not certify other variants or phone speed.

Stop/backgrounding terminates and unloads the worker, retaining model files and interrupted messages. Load again to continue. No SharedArrayBuffer or cross-origin-isolation assumption.

Conversations use an explicit model. Create a new conversation when changing models. The 512-token limit includes history, template and output; shorten your chat if it exceeds this limit.
