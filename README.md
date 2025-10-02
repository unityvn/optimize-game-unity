```markdown
# 🎮 Unity Game Optimization Guide

Khi phát triển game bằng Unity, tối ưu hóa (optimize) là bước quan trọng để đảm bảo **hiệu suất**, **trải nghiệm người chơi**, và **tính tương thích đa nền tảng**.  
Dưới đây là checklist các mảng cần tối ưu, kèm theo gợi ý thực hiện.

---

## 📦 1. Optimize Asset (Tài nguyên)
- **Texture & Sprite**
  - Giảm kích thước, nén (Compression).
  - Dùng đúng format (ETC2/ASTC cho Android, PVRTC cho iOS).
  - Sprite Atlas để giảm draw calls.
- **Model & Mesh**
  - Giảm poly count, tránh mesh quá chi tiết.
  - Dùng LOD (Level of Detail) cho model xa/gần.
- **Animation**
  - Baking animation khi có thể.
  - Giảm số lượng keyframe không cần thiết.
- **Audio**
  - Nén file (MP3/OGG).
  - Streaming nhạc nền dài thay vì load toàn bộ.

---

## 🎨 2. Optimize Rendering (Hiển thị)
- **Batching**
  - Static Batching cho object cố định.
  - Dynamic Batching hoặc GPU Instancing cho object lặp lại.
- **Lighting**
  - Bake lightmap thay vì realtime.
  - Sử dụng Mixed/Static light khi có thể.
  - Giảm số lượng shadow real-time.
- **Shader & Material**
  - Dùng shader mobile-friendly.
  - Giảm số lượng material, combine khi có thể.
- **Camera & Post-processing**
  - Hạn chế hiệu ứng nặng (Bloom, SSAO, Motion Blur).
  - Chỉnh clipping plane hợp lý, chỉ render cần thiết.
- **Overdraw (2D)**
  - Tránh sprite trong suốt chồng nhiều lớp.
  - Sắp xếp layer hợp lý.

---

## ⚙️ 3. Optimize Code & Logic
- **Garbage Collection (GC)**
  - Tránh tạo object liên tục trong `Update()`.
  - Object Pooling thay vì `Instantiate`/`Destroy`.
- **Update/FixedUpdate**
  - Hạn chế logic nặng trong `Update()`.
  - Dùng Coroutine hoặc event thay cho polling.
- **Physics**
  - Giảm số lượng Rigidbody/Collider.
  - Sử dụng layer collision matrix để tránh tính toán thừa.
  - Điều chỉnh `Fixed Timestep` phù hợp.
- **AI/Pathfinding**
  - Chia nhỏ xử lý theo frame.
  - Cache kết quả khi có thể.

---

## 🧠 4. Optimize Memory
- Giải phóng asset không dùng với `Resources.UnloadUnusedAssets` hoặc `Addressables.Release`.
- Tránh giữ reference asset không cần thiết.
- Load theo nhu cầu với **Addressables/Asset Bundles** thay vì nhét hết vào build.

---

## 📱 5. Optimize Build & Platform
- **Build Settings**
  - Chọn kiến trúc CPU đúng (ARMv7/ARM64).
  - Bật Strip Engine Code để giảm dung lượng.
- **Quality Settings**
  - Tùy platform mà giảm hiệu ứng hoặc texture size.
  - Giới hạn FPS hợp lý (ví dụ: 30fps cho game casual mobile).
- **IL2CPP & Code Stripping**
  - Bật Managed Stripping Level để loại bỏ code không dùng.

---

## ✅ Checklist nhanh
- [ ] Texture nén và atlas hóa.  
- [ ] Model tối ưu poly, có LOD.  
- [ ] Lightmap đã bake, hạn chế realtime shadow.  
- [ ] Shader/material được giảm thiểu.  
- [ ] Sử dụng batching (static/dynamic/GPU instancing).  
- [ ] Object pooling thay cho instantiate/destroy.  
- [ ] Physics và AI được tối ưu.  
- [ ] Addressables/AssetBundle để quản lý memory.  
- [ ] Build settings phù hợp nền tảng.  
- [ ] Managed Stripping Level bật để giảm code thừa.  

---

✨ Tối ưu hóa không phải là một bước cuối cùng, mà là **quá trình liên tục** trong suốt vòng đời phát triển game.  
Hãy profile thường xuyên, phát hiện bottleneck và xử lý kịp thời.
```
