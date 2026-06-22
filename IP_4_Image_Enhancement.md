

# 📘 B.Tech 6th Semester — Exam Preparation

**Author:** Rishav Raj | **Semester:** 6th Sem | **Subject:** Image Processing — Image Enhancement | **Marks per Answer:** 5–10 Marks

---

## 📌 How to Use This Document

- Each answer is structured for **5–10 marks** university exam questions.

- Every answer covers **1-2 pages** of content with proper depth.

- Format includes: **Definition → Explanation → Key Points → Diagram/Example → Conclusion**

---

---

## ❓ Question 1: What are median filters? What is image enhancement? What is image restoration? Differentiate between image enhancement and image restoration. What are image negatives? What is the equation for obtaining a negative image? Explain the operation of a median filter. (Numerical on median filter). Explain gray-level slicing.

### ✅ Answer:

#### 📖 Definition / Introduction

**Image enhancement** improves the visual appearance of an image subjectively, while **image restoration** recovers a degraded image objectively using a mathematical model. **Median filters** are non-linear spatial filters that replace each pixel with the median of its neighbourhood, excelling at removing salt-and-pepper noise. **Image negatives** reverse the intensity scale, and **grey-level slicing** highlights a specific intensity range while suppressing others.

---

#### 📝 Detailed Explanation

**Key Point 1: Image Enhancement vs. Image Restoration**

> **Image Enhancement:** The process of manipulating an image so that the result is more suitable for a specific application than the original. It is **subjective** — there is no unique "correct" output. Techniques include contrast stretching, histogram equalization, sharpening, and smoothing.
>
> **Image Restoration:** The process of recovering an image that has been degraded by a known or estimated degradation function. It is **objective** — based on mathematical/statistical models of the degradation process. Techniques include inverse filtering, Wiener filtering, and constrained least-squares filtering.
>
> | Feature | Image Enhancement | Image Restoration |
> |---------|------------------|-------------------|
> | **Goal** | Improve visual quality | Recover original image |
> | **Approach** | Subjective, heuristic | Objective, model-based |
> | **Knowledge needed** | None about degradation | Degradation model required |
> | **Evaluation** | Visual (human judgement) | Mathematical (MSE, PSNR) |
> | **Techniques** | Histogram eq., sharpening | Wiener filter, inverse filter |
> | **Result** | May not look like original | Approximates the original |

**Key Point 2: Image Negatives**

> An **image negative** (also called complement) reverses the grey levels of an image — dark becomes light and vice versa.
>
> **Equation:** For an image with intensity range [0, L−1]:
>
> **s = (L − 1) − r**
>
> where r is the input intensity and s is the output intensity.
>
> For an 8-bit image (L = 256): **s = 255 − r**
>
> - r = 0 (black) → s = 255 (white)
> - r = 255 (white) → s = 0 (black)
>
> **Application:** Enhancing white/light details embedded in dark regions (e.g., mammogram analysis where tumours appear lighter in the negative).

**Key Point 3: Median Filter — Operation**

> The **median filter** is a non-linear spatial filter that replaces each pixel value with the **median** of the intensity values in its neighbourhood.
>
> **Algorithm:**
> 1. Define a window (typically 3×3, 5×5, or 7×7) centred on pixel (x, y).
> 2. Extract all pixel values within the window.
> 3. Sort the values in ascending order.
> 4. Replace the centre pixel with the **middle value** (median) of the sorted list.
> 5. Move the window to the next pixel and repeat.
>
> **Properties:**
> - Excellent at removing **salt-and-pepper (impulse) noise** while preserving edges.
> - Does NOT blur edges (unlike mean/averaging filters).
> - The output value is always an existing pixel value (no new values created).
> - For an n×n window, the median is at position (n²+1)/2 in the sorted list.

**Key Point 4: Numerical on Median Filter**

> Given a 3×3 neighbourhood:
> ```
> ┌─────┬─────┬─────┐
> │  10 │  15 │  20 │
> ├─────┼─────┼─────┤
> │  25 │ 200 │  30 │   ← centre pixel = 200 (noise spike)
> ├─────┼─────┼─────┤
> │  22 │  18 │  28 │
> └─────┴─────┴─────┘
> ```
> Sorted values: {10, 15, 18, 20, **22**, 25, 28, 30, 200}
>
> Median = 5th value = **22**
>
> The noisy pixel 200 is replaced by 22 — noise effectively removed!

**Key Point 5: Grey-Level Slicing**

> **Grey-level slicing** (intensity-level slicing) highlights a specific range of grey levels in an image. Two approaches:
>
> **(a) Without background preservation:**
> - Pixels in the range [A, B] → set to a high value (e.g., 255).
> - All other pixels → set to a low value (e.g., 0).
> - Result: Binary-like image highlighting the range.
>
> **(b) With background preservation:**
> - Pixels in the range [A, B] → set to a high value (e.g., 255).
> - All other pixels → remain at their original values.
> - Result: Highlighted range with background intact.
>
> **Application:** Highlighting specific features like water bodies (specific grey range) in satellite imagery, or specific tissue types in medical images.

---

#### 📊 Diagram / Table (if applicable)

```
  Image Negative:
  Input:   0 ──────────────── 255      Output: 255 ──────────────── 0
           Black    Grey    White              White    Grey    Black
  s = 255 - r (linear reversal)

  Median Filter vs. Mean Filter:
  ┌──────────────┬───────────────────┬───────────────────┐
  │ Feature      │ Median Filter     │ Mean Filter       │
  ├──────────────┼───────────────────┼───────────────────┤
  │ Type         │ Non-linear        │ Linear            │
  │ Noise type   │ Salt & pepper     │ Gaussian noise    │
  │ Edge preserv.│ Good              │ Poor (blurs edges)│
  │ New values?  │ No                │ Yes (averages)    │
  │ Speed        │ Slower (sorting)  │ Faster            │
  └──────────────┴───────────────────┴───────────────────┘

  Grey-Level Slicing:
  (a) Without background:          (b) With background:
  s ↑                              s ↑
  L ┤      ████                    L ┤      ████
    │      ████                      │     ╱████╲
    │      ████                      │    ╱  ████ ╲
  0 ┤──────    ──────              0 ┤───╱        ╲───
    └──┬───A──B─┬───→ r              └──┬───A──B──┬──→ r
```

---

#### 💡 Example

> A chest X-ray image has low contrast in the lung region. Applying the **image negative** makes subtle white lesions in the dark lung fields more visible. A **median filter (5×5)** removes salt-and-pepper noise from a scanned document without blurring the text edges. **Grey-level slicing** with range [100, 150] on a satellite image highlights water bodies that have grey levels in this range.

---

#### 🔚 Conclusion

> Image enhancement and restoration are two complementary approaches — enhancement improves visual quality subjectively, while restoration recovers degraded images objectively. The median filter is the preferred tool for salt-and-pepper noise removal due to its edge-preserving property. Image negatives reverse intensities using s = (L−1) − r, useful for revealing details in dark regions. Grey-level slicing highlights specific intensity ranges for targeted analysis, available with or without background preservation.

---

---

## ❓ Question 2: Discuss the limiting effect of repeatedly applying a 3×3 spatial filter to a digital image. What is the equation of the Wiener filter used to reconstruct an image blurred by this type of degradation? What is Wiener filtering?

### ✅ Answer:

#### 📖 Definition / Introduction

When a **3×3 spatial averaging (smoothing) filter** is applied repeatedly to a digital image, it produces progressively greater blurring that eventually converges to a **uniform (constant) image**. The **Wiener filter** (also called the minimum mean square error filter) is the optimal linear filter for restoring images degraded by such blurring in the presence of noise. It balances noise reduction against deblurring.

---

#### 📝 Detailed Explanation

**Key Point 1: Limiting Effect of Repeated 3×3 Filtering**

> When a 3×3 averaging filter (each weight = 1/9) is applied **once**, each pixel becomes the average of its 9 neighbours — moderate smoothing/blurring occurs.
>
> **Repeated application:**
> - **1st application:** Slight blur, reduces high-frequency noise. Effective neighbourhood = 3×3.
> - **2nd application:** More blur. Effective neighbourhood = 5×5 (each output pixel is influenced by a 5×5 region of the original).
> - **k-th application:** Effective neighbourhood grows to approximately **(2k+1) × (2k+1)**. The image becomes progressively more blurred.
> - **As k → ∞:** The image converges to a **constant value equal to the mean grey level** of the original image. All spatial detail is lost.
>
> **Mathematically:** Repeated application of a 3×3 averaging filter is equivalent to **convolution** of the original image with a progressively wider Gaussian-like kernel. In the frequency domain, this corresponds to repeated multiplication by the filter's transfer function H(u,v), which attenuates high frequencies. As k → ∞, |H(u,v)|^k → 0 for all (u,v) except (0,0), leaving only the DC component.
>
> **Key insight:** Each application of the 3×3 filter is equivalent to a convolution in the spatial domain (multiplication in the frequency domain). The k-th application gives an effective filter H_eff(u,v) = [H(u,v)]^k, which approaches zero for all non-DC frequencies.

**Key Point 2: Wiener Filter**

> **Wiener filtering** (minimum mean square error filtering) is a restoration technique that finds the estimate f̂ of the original image that minimizes the **mean square error** E{|f − f̂|²}.
>
> **The degradation model:** g(x,y) = h(x,y) ∗ f(x,y) + η(x,y)
>
> In frequency domain: **G(u,v) = H(u,v) · F(u,v) + N(u,v)**
>
> where g = degraded image, f = original image, h = degradation function (PSF), η = additive noise.
>
> **Wiener Filter Equation:**
>
> **F̂(u,v) = [H*(u,v) / (|H(u,v)|² + S_η(u,v)/S_f(u,v))] · G(u,v)**
>
> Or equivalently:
>
> **F̂(u,v) = [1/H(u,v)] · [|H(u,v)|² / (|H(u,v)|² + S_η/S_f)] · G(u,v)**
>
> Where:
> - H*(u,v) = complex conjugate of H(u,v)
> - |H(u,v)|² = H(u,v) · H*(u,v)
> - S_η(u,v) = power spectrum of the noise
> - S_f(u,v) = power spectrum of the original (undegraded) image
> - S_η/S_f = noise-to-signal power ratio (NSR)
>
> **Simplified form (when NSR is a constant K):**
>
> **F̂(u,v) = [H*(u,v) / (|H(u,v)|² + K)] · G(u,v)**

**Key Point 3: Properties of Wiener Filter**

> - When **noise = 0** (S_η = 0): Wiener filter reduces to the **inverse filter** F̂ = G/H.
> - When **noise dominates** (S_η >> S_f · |H|²): Wiener filter acts as a **smoothing filter**, suppressing noise.
> - The Wiener filter **automatically balances** noise suppression and deblurring.
> - It never amplifies noise as the inverse filter does at frequencies where |H| is small.
> - It requires knowledge of S_η and S_f, which are often estimated or approximated.

---

#### 📊 Diagram / Table (if applicable)

```
  Repeated Application of 3×3 Averaging Filter:

  Original       k=1          k=3          k=10         k→∞
  ┌────────┐   ┌────────┐   ┌────────┐   ┌────────┐   ┌────────┐
  │Sharp   │   │Slightly│   │Moderate│   │Heavily │   │Uniform │
  │details │→  │blurred │→  │blurred │→  │blurred │→  │grey    │
  │visible │   │        │   │        │   │        │   │(mean)  │
  └────────┘   └────────┘   └────────┘   └────────┘   └────────┘
  Effective:    3×3          7×7          21×21        All pixels
  neighbourhood

  In frequency domain:
  |H_eff(u,v)| = |H(u,v)|^k → 0 for (u,v) ≠ (0,0) as k → ∞

  Wiener Filter Block Diagram:
  Original f → [Degradation H] → + → Degraded g → [Wiener Filter] → Restored f̂
                                 ↑
                              Noise η

  Wiener Filter:               
  F̂(u,v) = H*(u,v) · G(u,v)     ← combines inverse filtering
            ─────────────────       and noise suppression
            |H|² + S_η/S_f

  Wiener vs. Inverse Filter:
  ┌──────────────┬─────────────────┬──────────────────┐
  │ Feature      │ Inverse Filter  │ Wiener Filter    │
  ├──────────────┼─────────────────┼──────────────────┤
  │ Formula      │ F̂ = G/H         │ F̂ = H*G/(|H|²+K)│
  │ Noise handling│ Amplifies noise │ Suppresses noise │
  │ Stability    │ Unstable (H≈0)  │ Stable           │
  │ Optimality   │ Not optimal     │ MSE optimal      │
  └──────────────┴─────────────────┴──────────────────┘
```

---

#### 💡 Example

> An image blurred by 5 repeated applications of a 3×3 averaging filter has an effective PSF approximately equal to an 11×11 Gaussian. To restore it, the Wiener filter is applied in the frequency domain: G(u,v) is computed via FFT, the known H(u,v) = [H₃ₓ₃(u,v)]⁵ is used, and the NSR K is estimated (e.g., K = 0.01). The result F̂ = H*G/(|H|²+0.01) recovers most of the lost detail while keeping noise amplification under control.

---

#### 🔚 Conclusion

> Repeated application of a 3×3 spatial averaging filter progressively blurs the image, with the effective neighbourhood growing as (2k+1)×(2k+1), until the image converges to a uniform constant (the mean grey level). The Wiener filter is the optimal linear restoration filter that minimizes mean square error by balancing deblurring against noise amplification. Its equation F̂(u,v) = H*G/(|H|²+S_η/S_f) elegantly reduces to inverse filtering when noise is absent and to smoothing when noise dominates.

---

---

## ❓ Question 3: Explain unsharp masking and high-boost filtering. What is the expression of the Laplacian operator for an image of two variables?

### ✅ Answer:

#### 📖 Definition / Introduction

**Unsharp masking** and **high-boost filtering** are image sharpening techniques that enhance edges and fine details by emphasizing high-frequency components. The **Laplacian operator** is a second-order derivative operator used for edge detection and image sharpening, defined as the sum of second partial derivatives.

---

#### 📝 Detailed Explanation

**Key Point 1: Unsharp Masking**

> **Unsharp masking** sharpens an image by subtracting a blurred (smoothed) version from the original:
>
> **Step 1:** Blur the original image f(x,y) to get f̄(x,y) (using a Gaussian or averaging filter).
>
> **Step 2:** Subtract the blurred image from the original to get the **mask** (detail/high-frequency component):
> g_mask(x,y) = f(x,y) − f̄(x,y)
>
> **Step 3:** Add the mask back to the original:
> g(x,y) = f(x,y) + k · g_mask(x,y)
>
> where k is a scaling constant (typically k = 1 for standard unsharp masking).
>
> **Combined formula:**
> **g(x,y) = f(x,y) + k · [f(x,y) − f̄(x,y)]**
>
> The "unsharp" in the name refers to the blurred image used in the process — it is the "unsharp" version.

**Key Point 2: High-Boost Filtering**

> **High-boost filtering** is a generalization of unsharp masking where the original image is amplified by a factor A before subtracting the blurred version:
>
> **g(x,y) = A · f(x,y) − f̄(x,y)**
>
> Which can be rewritten as:
>
> **g(x,y) = (A−1) · f(x,y) + [f(x,y) − f̄(x,y)]**
> **g(x,y) = (A−1) · f(x,y) + g_mask(x,y)**
>
> **Special cases:**
> - **A = 1:** Standard unsharp masking: g = f − f̄ = mask (only high-freq components).
> - **A > 1:** Original image is partially preserved along with enhanced details.
> - **A >> 1:** Result approaches the original image (little enhancement).
>
> High-boost filtering provides more control over the sharpening level than simple unsharp masking.

**Key Point 3: Laplacian Operator**

> The **Laplacian** is a second-order derivative operator defined as the sum of second partial derivatives:
>
> **∇²f = ∂²f/∂x² + ∂²f/∂y²**
>
> **Discrete approximation (for digital images):**
>
> ∂²f/∂x² ≈ f(x+1, y) + f(x−1, y) − 2f(x, y)
>
> ∂²f/∂y² ≈ f(x, y+1) + f(x, y−1) − 2f(x, y)
>
> **∇²f(x,y) = f(x+1,y) + f(x−1,y) + f(x,y+1) + f(x,y−1) − 4f(x,y)**
>
> **3×3 Laplacian kernel (4-neighbour):**
> ```
> [ 0  1  0]       or including diagonals:  [ 1  1  1]
> [ 1 -4  1]       (8-neighbour Laplacian)   [ 1 -8  1]
> [ 0  1  0]                                 [ 1  1  1]
> ```
>
> **Image sharpening using Laplacian:**
> g(x,y) = f(x,y) − ∇²f(x,y) (if centre coefficient is negative)
> g(x,y) = f(x,y) + ∇²f(x,y) (if centre coefficient is positive)

---

#### 📊 Diagram / Table (if applicable)

```
  Unsharp Masking Pipeline:
  f(x,y) ─────────────────────────────────(+)───→ g(x,y)
     │                                     ↑
     └──→ [Blur/Smooth] ──→ f̄(x,y) ──→ (−) ──→ g_mask ──→ ×k ──┘
                                          (f − f̄ = mask)

  High-Boost Filtering:
  f(x,y) ──→ × A ──→ (−) ──→ g(x,y) = A·f − f̄
                      ↑
  f(x,y) ──→ [Blur] ──→ f̄(x,y)

  Laplacian Kernels:
  4-neighbour:    8-neighbour:    Negative centre:
  [ 0  1  0]     [ 1  1  1]     [ 0 -1  0]
  [ 1 -4  1]     [ 1 -8  1]     [-1  4 -1]
  [ 0  1  0]     [ 1  1  1]     [ 0 -1  0]

  Sharpening: g = f - ∇²f   or   g = f + ∇²f
  (depends on sign convention of Laplacian kernel)

  Comparison:
  ┌─────────────────┬─────────────────┬──────────────────┐
  │ Technique       │ Formula         │ Control Parameter│
  ├─────────────────┼─────────────────┼──────────────────┤
  │ Unsharp masking │ g = f + k(f−f̄)  │ k (mask weight)  │
  │ High-boost      │ g = Af − f̄      │ A (amplification)│
  │ Laplacian       │ g = f − ∇²f     │ None (fixed)     │
  └─────────────────┴─────────────────┴──────────────────┘
```

---

#### 💡 Example

> A blurry photograph is sharpened using unsharp masking: a 5×5 Gaussian blur creates f̄, the mask g_mask = f − f̄ contains edges and details, and adding k=1.5 times the mask back produces a noticeably sharper image. The Laplacian ∇²f of the same image reveals all edges (positive and negative intensity transitions), and adding f + ∇²f enhances edge contrast.

---

#### 🔚 Conclusion

> Unsharp masking enhances details by subtracting a blurred version and adding the high-frequency mask back. High-boost filtering generalizes this by introducing an amplification factor A for more control. The Laplacian operator ∇²f = ∂²f/∂x² + ∂²f/∂y² provides isotropic (direction-independent) second-order edge detection and can be implemented as a 3×3 kernel with centre coefficient −4 or −8. All three techniques serve the common purpose of image sharpening by emphasizing high-frequency content.

---

---

## ❓ Question 4: Briefly describe smoothing linear spatial filtering. What is the bit-plane slicing method? What is spatial filtering?

### ✅ Answer:

#### 📖 Definition / Introduction

**Spatial filtering** is the process of modifying pixel values by applying a filter mask (kernel) to the image in the spatial domain. **Smoothing linear spatial filtering** uses averaging-type kernels to reduce noise and blur images. **Bit-plane slicing** decomposes an image into its constituent bit planes, revealing the contribution of each bit to the overall image appearance.

---

#### 📝 Detailed Explanation

**Key Point 1: Spatial Filtering**

> **Spatial filtering** operates directly on the pixel values of an image by moving a filter mask (kernel) across the image and computing a new pixel value at each position based on the mask coefficients and the neighbourhood pixel values.
>
> **Process:**
> 1. A mask (kernel) of size m × n is placed over each pixel (x, y).
> 2. The mask coefficients are multiplied with the corresponding pixel values.
> 3. The products are summed (for linear filters) to produce the output at (x, y).
>
> **g(x,y) = Σᵢ Σⱼ w(i,j) · f(x+i, y+j)**
>
> **Types:**
> - **Linear filters:** Output = weighted sum (averaging, Gaussian, Laplacian).
> - **Non-linear filters:** Output = non-linear function (median, max, min).
> - **Smoothing filters:** Reduce noise, blur (averaging, Gaussian).
> - **Sharpening filters:** Enhance edges (Laplacian, gradient).

**Key Point 2: Smoothing Linear Spatial Filtering**

> **Smoothing (low-pass) filters** blur the image and reduce noise by replacing each pixel with a weighted average of its neighbourhood.
>
> **(a) Box/Averaging Filter:**
> All coefficients are equal: w(i,j) = 1/(m×n)
>
> 3×3 averaging kernel: (1/9) × [1 1 1; 1 1 1; 1 1 1]
>
> **(b) Weighted Averaging Filter:**
> Centre pixel gets more weight than neighbours:
>
> (1/16) × [1 2 1; 2 4 2; 1 2 1]
>
> **(c) Gaussian Filter:**
> Coefficients follow a 2D Gaussian distribution:
> w(x,y) = (1/2πσ²) · e^(−(x²+y²)/2σ²)
>
> Provides smoother results than box filters (no ringing artefacts).
>
> **Properties:**
> - Larger kernels → more smoothing/blurring.
> - Reduces Gaussian noise effectively.
> - Blurs edges (disadvantage).
> - Computationally simple (O(m×n) per pixel, or O(1) with integral images for box filters).

**Key Point 3: Bit-Plane Slicing**

> An 8-bit image has pixel values from 0 to 255. Each pixel can be represented as an 8-bit binary number. **Bit-plane slicing** separates the image into 8 binary images (bit planes), one for each bit position.
>
> - **Bit 7 (MSB — Most Significant Bit):** Carries the most visual information. Contains the coarse structure of the image.
> - **Bit 6:** Second most significant — significant visual contribution.
> - **Bit 5, 4:** Moderate contribution to visual appearance.
> - **Bit 3, 2, 1:** Decreasing visual contribution.
> - **Bit 0 (LSB — Least Significant Bit):** Contains the least visual information. Appears as random noise.
>
> **Extraction:** Bit plane i of pixel value v = (v >> i) & 1 (bitwise shift and AND).
>
> **Applications:**
> - **Image compression:** Discard lower bit planes (e.g., keeping only top 4–5 planes).
> - **Steganography/Watermarking:** Hide data in the LSB plane (imperceptible change).
> - **Image analysis:** Understanding the contribution of each bit level.
> - **Texture analysis:** Certain bit planes reveal texture patterns.

---

#### 📊 Diagram / Table (if applicable)

```
  Spatial Filtering Process:
  ┌──────────────┐     ┌────────┐
  │ Image f(x,y) │ ──→ │ Kernel │ ──→ g(x,y) = Σ w(i,j)·f(x+i,y+j)
  └──────────────┘     │ w(i,j) │
                       └────────┘

  Smoothing Kernels:
  Box Filter:         Weighted Average:     Gaussian (approx):
  ┌───┬───┬───┐      ┌───┬───┬───┐        ┌───┬───┬───┐
  │1/9│1/9│1/9│      │1  │ 2 │ 1 │ ×1/16  │ 1 │ 2 │ 1 │ ×1/16
  ├───┼───┼───┤      ├───┼───┼───┤        ├───┼───┼───┤
  │1/9│1/9│1/9│      │2  │ 4 │ 2 │        │ 2 │ 4 │ 2 │
  ├───┼───┼───┤      ├───┼───┼───┤        ├───┼───┼───┤
  │1/9│1/9│1/9│      │1  │ 2 │ 1 │        │ 1 │ 2 │ 1 │
  └───┴───┴───┘      └───┴───┴───┘        └───┴───┴───┘

  Bit-Plane Slicing (8-bit image):
  Pixel value 167 = 10100111 in binary

  Bit 7 (MSB): 1  ← Most visual info
  Bit 6:       0
  Bit 5:       1
  Bit 4:       0
  Bit 3:       0
  Bit 2:       1
  Bit 1:       1
  Bit 0 (LSB): 1  ← Least visual info (noise-like)

  Visual Contribution:
  Plane 7 > Plane 6 > ... > Plane 1 > Plane 0
  (Coarse)                              (Fine/Noise)
```

---

#### 💡 Example

> A noisy medical image is filtered using a 5×5 Gaussian smoothing filter (σ=1.0). The noise is significantly reduced, though edges become slightly blurred. Bit-plane slicing of a portrait image shows: Plane 7 captures the face outline and major features, Planes 5–6 add medium details, and Planes 0–2 appear as random noise. A watermark is embedded in Plane 0 (LSB) — changing the least significant bit by 1 produces an imperceptible change (intensity changes by at most 1 out of 255).

---

#### 🔚 Conclusion

> Spatial filtering applies kernels directly to pixel neighbourhoods — smoothing filters reduce noise through averaging while blurring edges. The Gaussian filter provides the smoothest results among linear smoothing filters. Bit-plane slicing decomposes an image into its binary components, revealing that the MSB planes carry most visual information while LSB planes appear noise-like. These concepts are fundamental to understanding noise reduction, image compression, and data hiding in digital images.

---

---

## ❓ Question 5: What is understood by spatial domain representation? Compute the inverse Fourier transform using the forward transform algorithm.

### ✅ Answer:

#### 📖 Definition / Introduction

**Spatial domain representation** refers to describing and manipulating an image directly in terms of its pixel values at specific spatial coordinates (x, y), as opposed to its frequency-domain representation. Computing the **inverse DFT using the forward DFT algorithm** is an elegant mathematical trick that avoids implementing a separate IDFT routine — the same FFT code can be reused.

---

#### 📝 Detailed Explanation

**Key Point 1: Spatial Domain Representation**

> In the spatial domain, a digital image is represented as a 2D function **f(x, y)**, where:
> - **(x, y)** are discrete spatial coordinates (pixel locations).
> - **f(x, y)** is the intensity/grey level at that location.
>
> The image is a matrix of M rows × N columns, with each element being a pixel value.
>
> **Spatial domain operations** work directly on pixel values:
> - **Point operations:** Transform each pixel independently: s = T(r).
>   - Examples: Negative, log transform, power-law transform, contrast stretching.
> - **Neighbourhood operations:** Transform each pixel based on its local neighbourhood.
>   - Examples: Smoothing, sharpening, median filtering.
>
> **General form:** g(x,y) = T[f(x,y)]
>
> where T is an operator defined over a neighbourhood of (x, y).

**Key Point 2: Computing IDFT Using Forward DFT**

> The forward and inverse DFT for 1D are:
>
> **Forward DFT:** F(u) = (1/N) Σ[x=0 to N−1] f(x) · e^(−j2πux/N)
>
> **Inverse DFT:** f(x) = Σ[u=0 to N−1] F(u) · e^(+j2πux/N)
>
> **Key Observation:** The IDFT can be computed using the forward DFT as follows:
>
> **Step 1:** Take the complex conjugate of F(u): F*(u)
>
> **Step 2:** Apply the forward DFT to F*(u): DFT{F*(u)} = G(u)
>
> **Step 3:** Take the complex conjugate of the result: G*(u)
>
> **Step 4:** Divide by N: f(x) = G*(x) / N ... wait, let's be more precise.
>
> **Derivation:**
>
> f(x) = Σ[u] F(u) · e^(j2πux/N)
>
> Taking conjugate of both sides:
>
> f*(x) = Σ[u] F*(u) · e^(−j2πux/N) = N × DFT{F*(u)}
>
> Therefore: f(x) = [N × DFT{F*(u)}]*  → if f is real, f* = f.
>
> **Algorithm:**
> 1. Conjugate the input: F*(u)
> 2. Apply forward DFT (FFT): compute DFT{F*(u)}
> 3. Conjugate the result
> 4. Divide by N
>
> **f(x) = (1/N) · [DFT{F*(u)}]***
>
> This means we can use the **same FFT routine** for both forward and inverse transforms!

---

#### 📊 Diagram / Table (if applicable)

```
  Spatial Domain Representation:
  ┌──────────────────────────────────────┐
  │  f(x,y) = M × N matrix of pixels    │
  │                                      │
  │  f(0,0)   f(0,1)   ...  f(0,N-1)    │
  │  f(1,0)   f(1,1)   ...  f(1,N-1)    │
  │   ...      ...           ...         │
  │  f(M-1,0) f(M-1,1) ... f(M-1,N-1)   │
  └──────────────────────────────────────┘

  IDFT using Forward DFT:

  F(u) ──→ [Conjugate] ──→ F*(u) ──→ [Forward DFT/FFT] ──→ G(x)
                                                              │
                                                    [Conjugate + ÷N]
                                                              │
                                                              ↓
                                                            f(x)

  Proof Summary:
  IDFT{F(u)} = f(x) = Σ F(u)·e^(j2πux/N)

  Conjugate:
  f*(x) = Σ F*(u)·e^(-j2πux/N) = N · DFT{F*(u)}
  
  Therefore:
  f(x) = (1/N) · [DFT{F*(u)}]*
```

---

#### 💡 Example

> Given F(u) = {4, 1−j, 0, 1+j} for N=4:
> 1. Conjugate: F*(u) = {4, 1+j, 0, 1−j}
> 2. Apply forward DFT to F*: DFT{F*} = {(1/4)(4+1+j+0+1−j), ...} = compute using FFT
> 3. Conjugate the result
> 4. Divide by N = 4
>
> This gives f(x) = {1, 2, 1, 0} — the original sequence, computed entirely using the forward FFT algorithm.

---

#### 🔚 Conclusion

> The spatial domain represents images as matrices of pixel values at discrete coordinates, and spatial domain operations work directly on these values. The elegant relationship between forward and inverse DFT allows the IDFT to be computed using the same FFT algorithm: f(x) = (1/N)[DFT{F*(u)}]*. This saves implementation effort and memory, as only one FFT routine is needed for both directions of transformation.

---

---

## ❓ Question 6: What are spatial-domain and frequency-domain techniques? Explain masks (kernels). What is filtering in the frequency domain? Compare spatial-domain filtering and frequency-domain filtering.

### ✅ Answer:

#### 📖 Definition / Introduction

Image processing techniques are broadly classified into **spatial-domain techniques** (operating directly on pixels) and **frequency-domain techniques** (operating on the image's frequency representation). **Masks (kernels)** are small matrices used in spatial filtering. **Frequency-domain filtering** involves transforming the image to the frequency domain, modifying frequency components, and transforming back. Each approach has distinct advantages.

---

#### 📝 Detailed Explanation

**Key Point 1: Spatial-Domain Techniques**

> Operations performed directly on the pixel values f(x, y) of the image.
>
> **General form:** g(x, y) = T[f(x, y)]
>
> where T is an operator applied to the pixel and/or its neighbourhood.
>
> **Types:**
> - **Point processing:** s = T(r) — each pixel transformed independently.
> - **Mask/kernel processing:** Output depends on neighbourhood values.
>
> **Examples:** Contrast stretching, histogram equalization, spatial filtering (smoothing, sharpening, median filtering).

**Key Point 2: Masks (Kernels)**

> A **mask** (also called kernel, template, or window) is a small matrix of coefficients (weights) that is applied to each pixel's neighbourhood to produce the filtered output.
>
> **Structure:** An m × n array of coefficients w(i, j).
>
> **Application:** The mask is centred on each pixel (x, y). Each mask coefficient is multiplied by the corresponding image pixel, and all products are summed to produce the output at (x, y):
>
> g(x,y) = Σᵢ Σⱼ w(i,j) · f(x+i, y+j)
>
> **Common kernels:**
> - Averaging: all 1s (scaled) — smoothing
> - Laplacian: [0 1 0; 1 −4 1; 0 1 0] — edge detection
> - Sobel: gradient estimation — edge detection
> - Gaussian: bell-curve weights — smoothing

**Key Point 3: Frequency-Domain Filtering**

> In frequency-domain filtering:
>
> 1. **Transform** the image to frequency domain: F(u,v) = DFT{f(x,y)}
> 2. **Multiply** by a filter function: G(u,v) = F(u,v) · H(u,v)
> 3. **Inverse transform** back: g(x,y) = IDFT{G(u,v)}
>
> **Common frequency-domain filters:**
> - **Low-pass filters:** Preserve low frequencies, remove high (smoothing). Types: Ideal, Butterworth, Gaussian.
> - **High-pass filters:** Preserve high frequencies, remove low (sharpening). H_hp = 1 − H_lp.
> - **Band-pass/Band-reject filters:** Pass or reject a specific frequency band.
> - **Notch filters:** Remove specific frequency components (periodic noise).

**Key Point 4: Comparison**

> | Feature | Spatial Domain | Frequency Domain |
> |---------|---------------|-----------------|
> | **Domain** | Pixel values f(x,y) | Frequency coefficients F(u,v) |
> | **Operation** | Convolution with kernel | Multiplication by filter function |
> | **Equivalence** | Convolution in spatial = multiplication in frequency (Convolution Theorem) |
> | **Filter design** | Specify kernel coefficients | Specify frequency response curve |
> | **Intuition** | Direct — see effect on pixels | Indirect — think in frequencies |
> | **Computation (small kernel)** | Fast (O(m×n per pixel)) | Slower (FFT overhead) |
> | **Computation (large kernel)** | Slow (O(m×n grows) | Fast (always O(N log N)) |
> | **Flexibility** | Non-linear filters possible | Primarily linear filters |
> | **Visualization** | Kernel coefficients | Magnitude spectrum |
> | **Best for** | Small kernels, non-linear ops | Large kernels, freq. analysis |

---

#### 📊 Diagram / Table (if applicable)

```
  Spatial-Domain Filtering:
  f(x,y) ──→ [Convolve with kernel w] ──→ g(x,y)

  Frequency-Domain Filtering:
  f(x,y) ──→ [DFT] ──→ F(u,v) ──→ [× H(u,v)] ──→ G(u,v) ──→ [IDFT] ──→ g(x,y)

  Convolution Theorem (equivalence):
  g = f ∗ w   ↔   G = F · W
  (spatial convolution = frequency multiplication)

  Common Frequency-Domain Filters:
  |H(u,v)|
     1 ┤───────╲             Low-pass (Butterworth)
       │        ╲
       │         ╲─────
     0 ┤                → D(u,v) (distance from centre)

  |H(u,v)|
     1 ┤          ╱─────  High-pass
       │        ╱
       │───────╱
     0 ┤                → D(u,v)
```

---

#### 💡 Example

> **Spatial domain:** A 3×3 averaging kernel is convolved with a noisy image — simple, fast, direct. **Frequency domain:** The same smoothing can be achieved by computing the FFT of the image, multiplying by a Gaussian low-pass filter H(u,v) = e^(−D²/2D₀²), and computing the IFFT. For large kernels (e.g., 51×51), the frequency-domain approach is much faster because FFT complexity O(N²logN) doesn't depend on kernel size.

---

#### 🔚 Conclusion

> Spatial-domain techniques operate directly on pixels using kernels (masks), offering simplicity and supporting non-linear operations. Frequency-domain techniques transform the image, multiply by a filter function, and transform back, offering computational advantages for large kernels and intuitive frequency-based filter design. The Convolution Theorem guarantees equivalence: spatial convolution equals frequency multiplication. The choice between them depends on kernel size, filter type (linear/non-linear), and computational requirements.

---

---

## ❓ Question 7: What is a Quad-tree? What is salt-and-pepper noise? What is Gaussian noise? What is the frequency of an image? Discuss spatial resolution and grey-level resolution.

### ✅ Answer:

#### 📖 Definition / Introduction

A **Quad-tree** is a hierarchical data structure that recursively subdivides a 2D image into four quadrants. **Salt-and-pepper noise** and **Gaussian noise** are two common types of image noise. The **frequency of an image** relates to the rate of intensity change across the spatial domain. **Spatial resolution** and **grey-level resolution** define the detail and tonal range of a digital image respectively.

---

#### 📝 Detailed Explanation

**Key Point 1: Quad-tree**

> A **Quad-tree** is a tree data structure in which each internal node has exactly four children, representing the four quadrants (NW, NE, SW, SE) of a 2D region.
>
> **Construction:**
> 1. Start with the entire image as the root node.
> 2. If a region is **homogeneous** (satisfies a predicate P), it becomes a leaf node.
> 3. If not homogeneous, subdivide into 4 equal quadrants — each becomes a child node.
> 4. Recursively apply steps 2–3 to each child.
>
> **Applications:** Image segmentation (split-and-merge), image compression, spatial indexing, collision detection.
>
> **Depth** of the tree depends on image size: for a 2^n × 2^n image, maximum depth = n.

**Key Point 2: Salt-and-Pepper Noise**

> Also called **impulse noise**, it appears as random occurrences of pure **black (0) and white (255)** pixels scattered across the image.
>
> **Characteristics:**
> - Only extreme values (0 or 255) are affected.
> - Caused by transmission errors, dead pixels, or analog-to-digital converter errors.
> - **PDF:** p(z) = P_a for z = 0 (pepper), P_b for z = 255 (salt), 0 otherwise.
> - **Best filter:** Median filter (not mean filter — mean would blur the entire image).

**Key Point 3: Gaussian Noise**

> Gaussian noise has a probability density function (PDF) following the **normal/Gaussian distribution**:
>
> **p(z) = (1/√(2πσ²)) · e^(−(z−μ)²/2σ²)**
>
> where μ = mean (average), σ = standard deviation.
>
> **Characteristics:**
> - Affects ALL pixels — each pixel value is perturbed by a random amount.
> - Most common noise model in image processing.
> - Caused by sensor thermal noise, electronic circuit noise.
> - **Best filters:** Averaging filter, Gaussian filter, Wiener filter.

**Key Point 4: Frequency of an Image**

> **Image frequency** refers to the rate of change of pixel intensity across the spatial domain:
>
> - **Low frequency:** Regions where intensity changes **slowly** (smooth areas, uniform backgrounds). Found near the centre of the frequency spectrum.
> - **High frequency:** Regions where intensity changes **rapidly** (edges, fine details, textures, noise). Found far from the centre of the frequency spectrum.
> - **DC component** (zero frequency): The average intensity of the entire image — the value at F(0,0).
>
> The Fourier Transform reveals these frequency components as a 2D spectrum.

**Key Point 5: Spatial Resolution and Grey-Level Resolution**

> **Spatial Resolution:**
> - The smallest discernible detail in an image.
> - Measured in pixels per unit length (PPI, DPI) or line pairs per unit distance.
> - Determined by the number of pixels (M × N).
> - Higher spatial resolution → more pixels → finer detail → larger file.
>
> **Grey-Level Resolution:**
> - The smallest discernible change in grey level.
> - Determined by the number of bits per pixel (k): L = 2^k grey levels.
> - 8-bit = 256 levels, 4-bit = 16 levels, 1-bit = 2 levels (binary).
> - Higher grey-level resolution → smoother tonal gradations.
> - Too few levels → false contouring artefacts.
>
> **Trade-off:** For a fixed storage budget (M × N × k bits), increasing one resolution requires decreasing the other.

---

#### 📊 Diagram / Table (if applicable)

```
  Quad-tree:
  ┌──────┬──────┐           Root
  │  R1  │  R2  │          ╱    ╲
  ├──────┼──┬───┤        R1     R2...
  │  R3  │R4│R5 │              ╱╲
  │      ├──┼───┤            R4  R5...
  │      │R6│R7 │
  └──────┴──┴───┘

  Noise Types:
  Salt-and-Pepper:              Gaussian:
  ┌──────────────┐              ┌──────────────┐
  │ ·  ● ·  · ○ │              │ ~  ~  ~  ~  ~│
  │ ·  · ·  ● · │  ● = salt   │ ~  ~  ~  ~  ~│  ~ = slight random
  │ ○  · ·  · · │  ○ = pepper  │ ~  ~  ~  ~  ~│  perturbation on
  │ ·  · ○  · ● │              │ ~  ~  ~  ~  ~│  ALL pixels
  └──────────────┘              └──────────────┘

  Image Frequency:
  Low freq. (smooth)          High freq. (edges/detail)
  ░░░░░░░░░░░░░░░            ░█░█░█░█░█░█
  ░░░░░░░░░░░░░░░            █░█░█░█░█░█░
  ░░░░░░░░░░░░░░░            ░█░█░█░█░█░█
  (Slowly changing)           (Rapidly changing)
```

---

#### 💡 Example

> A scanned document with transmission errors has salt-and-pepper noise — random black and white dots. A 3×3 median filter removes them effectively. A low-light photograph has Gaussian noise — a grainy appearance over the entire image. A Gaussian smoothing filter (σ=1.5) reduces this noise. In the frequency spectrum of a landscape photo, the sky region contributes low frequencies (smooth) while tree branches contribute high frequencies (edges).

---

#### 🔚 Conclusion

> Quad-trees provide an efficient hierarchical representation for subdividing images. Salt-and-pepper noise consists of isolated extreme-value pixels best removed by median filtering, while Gaussian noise affects all pixels and is best reduced by averaging or Gaussian filtering. Image frequency describes how quickly intensity values change spatially. Spatial resolution (pixels per inch) and grey-level resolution (bits per pixel) together define the quality of a digital image, with a fundamental trade-off between the two for a fixed storage budget.

---

---

## ❓ Question 8: What is homomorphic filtering? Derive the equation for a homomorphic filter. Describe its applications.

### ✅ Answer:

#### 📖 Definition / Introduction

**Homomorphic filtering** is a frequency-domain technique used to simultaneously improve the **dynamic range compression** (reduce illumination variations) and **contrast enhancement** (enhance reflectance details) of an image. It is based on the illumination-reflectance model, where an image is modelled as the product of illumination and reflectance components. By operating in the log-frequency domain, these multiplicative components become separable and can be filtered independently.

---

#### 📝 Detailed Explanation

**Key Point 1: Illumination-Reflectance Model**

> An image f(x, y) can be modelled as:
>
> **f(x, y) = i(x, y) × r(x, y)**
>
> where:
> - **i(x, y)** = illumination component (light falling on the scene). Varies slowly → **low frequency**.
> - **r(x, y)** = reflectance component (light reflected by objects). Varies rapidly → **high frequency**.
>
> The challenge: i and r are multiplied, not added, so they cannot be separated by linear filtering directly.

**Key Point 2: Derivation of Homomorphic Filter**

> **Step 1: Take the natural logarithm** to convert multiplication to addition:
>
> z(x,y) = ln[f(x,y)] = ln[i(x,y)] + ln[r(x,y)]
>
> **Step 2: Apply the DFT (Fourier Transform):**
>
> Z(u,v) = FT{z(x,y)} = Fᵢ(u,v) + Fᵣ(u,v)
>
> where Fᵢ = FT{ln(i)} and Fᵣ = FT{ln(r)}.
>
> **Step 3: Apply the homomorphic filter H(u,v):**
>
> S(u,v) = H(u,v) · Z(u,v) = H(u,v) · Fᵢ(u,v) + H(u,v) · Fᵣ(u,v)
>
> **Step 4: Apply the Inverse DFT:**
>
> s(x,y) = IDFT{S(u,v)}
>
> **Step 5: Take the exponential** to reverse the logarithm:
>
> g(x,y) = e^(s(x,y))
>
> **The homomorphic filter H(u,v)** is designed such that:
> - **γ_L < 1** (at low frequencies): Attenuates illumination variations → compresses dynamic range.
> - **γ_H > 1** (at high frequencies): Amplifies reflectance variations → enhances contrast/details.
>
> **Filter function:**
>
> **H(u,v) = (γ_H − γ_L) × [1 − e^(−c·D²(u,v)/D₀²)] + γ_L**
>
> where D(u,v) = distance from origin, D₀ = cutoff frequency, c = sharpness constant.
>
> At D = 0: H = γ_L (attenuate low freq.)
> At D → ∞: H = γ_H (amplify high freq.)

---

#### 📊 Diagram / Table (if applicable)

```
  Homomorphic Filtering Pipeline:

  f(x,y) → [ln] → z(x,y) → [DFT] → Z(u,v) → [×H(u,v)] → S(u,v)
                                                               │
  g(x,y) ← [exp] ← s(x,y) ← [IDFT] ←────────────────────────┘

  f = i × r    →    ln(f) = ln(i) + ln(r)    →    Filter separately

  Homomorphic Filter Transfer Function:
  H(u,v)
  γ_H ┤              ─────────────── (enhance reflectance)
      │            ╱
      │          ╱
      │        ╱
  γ_L ┤──────╱                       (compress illumination)
      │
      └──────┬──────────────→ D(u,v) (frequency distance)
             D₀

  γ_L < 1: Reduces low-freq (illumination) variations
  γ_H > 1: Boosts high-freq (reflectance/detail)

  Before vs. After Homomorphic Filtering:
  ┌──────────────┐         ┌──────────────┐
  │ Bright │Dark │         │ Moderate│Mod.│
  │ area   │area │   →     │ even    │even│
  │(over-  │(under-│       │illumin. │illu│
  │exposed)│exposed│       │+ sharp  │+sh.│
  └──────────────┘         └──────────────┘
  (Uneven illumination)    (Uniform illumination + enhanced details)
```

---

#### 💡 Example

> A photograph taken in a room with a bright window: the area near the window is over-exposed while the room interior is dark. Applying homomorphic filtering with γ_L = 0.3 and γ_H = 1.5: the logarithm separates illumination (slowly varying bright/dark) from reflectance (object details). The filter attenuates the low-frequency illumination variations (making brightness more uniform) and enhances high-frequency reflectance (making interior objects clearer). The result shows both the window view and interior details clearly.

**Applications:**
> - Correcting **uneven illumination** in photographs and microscopy images.
> - **Medical imaging:** Enhancing X-rays, MRI scans with varying brightness.
> - **Satellite imagery:** Compensating for sun angle variations.
> - **Face recognition:** Normalizing lighting conditions across face images.
> - **Document image processing:** Handling pages photographed with shadows.
> - **Underwater imaging:** Correcting non-uniform lighting.

---

#### 🔚 Conclusion

> Homomorphic filtering elegantly handles the multiplicative nature of the illumination-reflectance model by applying a logarithm (converting multiplication to addition), filtering in the frequency domain to separately control low frequencies (illumination) and high frequencies (reflectance), and exponentiating the result. The filter simultaneously compresses dynamic range (γ_L < 1) and enhances local contrast (γ_H > 1), making it invaluable for images with uneven lighting conditions.

---

---

## ❓ Question 9: What are the steps involved in histogram equalization? Why is histogram equalization needed? Explain the histogram of a digital image. What is an image histogram? What do you mean by histogram specification? (Numerical on DC component of an image histogram).

### ✅ Answer:

#### 📖 Definition / Introduction

An **image histogram** is a graphical representation showing the distribution of pixel intensities in an image. **Histogram equalization** transforms pixel values to produce an approximately **uniform histogram**, maximizing contrast. **Histogram specification (matching)** transforms the image to have a **user-specified** histogram distribution. The **DC component** (F(0,0)) of an image represents the average intensity and is directly related to the histogram.

---

#### 📝 Detailed Explanation

**Key Point 1: Image Histogram**

> An image histogram h(rₖ) plots the number of pixels nₖ at each intensity level rₖ (k = 0, 1, ..., L−1).
>
> **Normalized histogram (PDF approximation):**
> p(rₖ) = nₖ / (M × N), where M × N = total pixels.
>
> Σ p(rₖ) = 1 (sum of all probabilities = 1).
>
> **Histogram characteristics:**
> - **Dark image:** Histogram concentrated on the left (low intensities).
> - **Bright image:** Histogram concentrated on the right (high intensities).
> - **Low-contrast image:** Histogram concentrated in a narrow range (middle).
> - **High-contrast image:** Histogram spread across the full range.

**Key Point 2: Why Histogram Equalization is Needed**

> - To improve **contrast** of images with narrow intensity distributions.
> - To **maximize information content** by utilizing the full dynamic range.
> - To produce images that are **perceptually better** for human viewers.
> - To **normalize** images for consistent appearance across different capture conditions.
> - As a **preprocessing step** before segmentation, recognition, or other operations.

**Key Point 3: Steps in Histogram Equalization**

> 1. **Compute the histogram** h(rₖ) = nₖ for k = 0, 1, ..., L−1.
> 2. **Compute the normalized histogram (PDF):** p(rₖ) = nₖ / (M × N).
> 3. **Compute the cumulative distribution function (CDF):**
>    s(k) = Σ[j=0 to k] p(rⱼ)
> 4. **Map old intensities to new values:**
>    sₖ = round[(L − 1) × s(k)]
> 5. **Apply the mapping:** Replace each pixel with intensity rₖ by the new value sₖ.
>
> **The transformation function:** s = T(r) = (L−1) × CDF(r)
>
> The result: the histogram of the output image is approximately **uniform** (flat), meaning all intensity levels are approximately equally represented.

**Key Point 4: Histogram Specification (Matching)**

> **Histogram specification** transforms an image so that its histogram matches a **user-defined target histogram** (not necessarily uniform).
>
> **Steps:**
> 1. Compute the CDF of the input image: s = T(r).
> 2. Compute the CDF of the desired (target) histogram: v = G(z).
> 3. Find the inverse mapping: z = G⁻¹(v).
> 4. Apply the composite mapping: z = G⁻¹(T(r)).
>
> This allows specific histogram shapes (e.g., bimodal, Gaussian) to be imposed on the image.

**Key Point 5: DC Component and Histogram**

> The **DC component** F(0,0) of the DFT is the **sum of all pixel values** (scaled by 1/MN):
>
> F(0,0) = (1/MN) Σ[x] Σ[y] f(x,y) = **mean intensity × MN** (with appropriate scaling)
>
> **Numerical Example:**
> An image of size 4×4 with pixel values:
> ```
> 1  2  3  4
> 5  6  7  8
> 1  3  5  7
> 2  4  6  8
> ```
> Sum = 1+2+3+4+5+6+7+8+1+3+5+7+2+4+6+8 = **72**
>
> F(0,0) = (1/16) × 72 = **4.5** (mean intensity)
>
> or with different DFT convention: F(0,0) = 72 (the raw sum).

---

#### 📊 Diagram / Table (if applicable)

```
  Histogram Equalization Process:

  Original Histogram          CDF (Transformation)      Equalized Histogram
  │ █                         │          ╱───           │  █ █ █ █ █ █ █ █
  │ █ █                       │        ╱                │  █ █ █ █ █ █ █ █
  │ █ █ █                     │      ╱                  │
  │ █ █ █ █                   │    ╱                    │
  │ █ █ █ █ █                 │  ╱                      │
  └──────────→ r              └──────────→ r            └──────────────→ s
  (Concentrated)              T(r) = (L-1)·CDF(r)       (Approximately uniform)

  Histogram Equalization Steps:
  ┌──────────────────────────────────────────────────────────────┐
  │ Step 1: h(rₖ) = count pixels at each intensity              │
  │ Step 2: p(rₖ) = h(rₖ) / (M×N)                              │
  │ Step 3: CDF(k) = Σ[j=0 to k] p(rⱼ)                         │
  │ Step 4: sₖ = round[(L-1) × CDF(k)]                          │
  │ Step 5: Replace rₖ → sₖ in image                             │
  └──────────────────────────────────────────────────────────────┘

  Histogram Specification:
  Input Image → T(r) → CDF_input → G⁻¹() → Matched Output
  Target Histogram → G(z) → CDF_target ──────┘

  DC Component:
  F(0,0) = (1/MN) Σ Σ f(x,y) = Mean intensity of the image
```

---

#### 💡 Example

> **Numerical — Histogram Equalization (3-bit, L=8):**
>
> | rₖ | nₖ | p(rₖ) | CDF | sₖ = round(7×CDF) |
> |----|-----|-------|-----|-----|
> | 0 | 790 | 0.19 | 0.19 | 1 |
> | 1 | 1023 | 0.25 | 0.44 | 3 |
> | 2 | 850 | 0.21 | 0.65 | 5 |
> | 3 | 656 | 0.16 | 0.81 | 6 |
> | 4 | 329 | 0.08 | 0.89 | 6 |
> | 5 | 245 | 0.06 | 0.95 | 7 |
> | 6 | 122 | 0.03 | 0.98 | 7 |
> | 7 | 81 | 0.02 | 1.00 | 7 |
>
> Mapping: 0→1, 1→3, 2→5, 3→6, 4→6, 5→7, 6→7, 7→7.
> The equalized histogram is more spread out across levels 1, 3, 5, 6, 7.

---

#### 🔚 Conclusion

> Image histograms are fundamental tools for understanding intensity distributions. Histogram equalization uses the CDF as a transformation function to redistribute intensities uniformly, maximizing contrast. Histogram specification extends this by allowing any desired output distribution. The DC component F(0,0) directly represents the average image intensity. These techniques are essential for image enhancement, normalization, and as preprocessing steps for further analysis.

---

---

## ❓ Question 10: Show how Prewitt and Sobel operators can be used to smooth/reduce the effect of noise.

### ✅ Answer:

#### 📖 Definition / Introduction

The **Prewitt** and **Sobel operators** are first-order derivative-based edge detection operators. While primarily used for detecting edges, they inherently incorporate a **smoothing component** perpendicular to the gradient direction, which helps reduce the effect of noise during edge detection. This built-in smoothing distinguishes them from simple difference operators.

---

#### 📝 Detailed Explanation

**Key Point 1: Prewitt Operator**

> The Prewitt operator uses two 3×3 kernels to compute the gradient in the x and y directions:
>
> **Gx (horizontal edges):**
> ```
> [-1  0  1]
> [-1  0  1]
> [-1  0  1]
> ```
>
> **Gy (vertical edges):**
> ```
> [-1 -1 -1]
> [ 0  0  0]
> [ 1  1  1]
> ```
>
> **Gradient magnitude:** |G| = |Gx| + |Gy| or √(Gx² + Gy²)
>
> **Smoothing in Prewitt:**
> - Each kernel can be decomposed as: **derivative × averaging**
> - Gx = [-1 0 1]ᵀ × [1 1 1] (derivative along x, **averaging along y**)
> - Gy = [1 1 1]ᵀ × [-1 0 1] (derivative along y, **averaging along x**)
> - The averaging component (3-point average: [1 1 1]) **smooths noise** in the direction perpendicular to the gradient, reducing the noise sensitivity of the edge detection.

**Key Point 2: Sobel Operator**

> The Sobel operator uses **weighted** averaging for stronger smoothing:
>
> **Gx:**
> ```
> [-1  0  1]
> [-2  0  2]
> [-1  0  1]
> ```
>
> **Gy:**
> ```
> [-1 -2 -1]
> [ 0  0  0]
> [ 1  2  1]
> ```
>
> **Smoothing in Sobel:**
> - Gx = [-1 0 1]ᵀ × [1 2 1] (derivative along x, **weighted averaging along y**)
> - Gy = [1 2 1]ᵀ × [-1 0 1] (derivative along y, **weighted averaging along x**)
> - The weighted average [1 2 1] is a **Gaussian-like** smoothing filter (more weight to the centre pixel), providing **better noise reduction** than the uniform [1 1 1] in Prewitt.
> - This gives the Sobel operator a slight **advantage over Prewitt** in noisy conditions.

**Key Point 3: How Smoothing Reduces Noise Effect**

> - Noise creates random, isolated intensity variations.
> - Simple finite differences (e.g., [−1 0 1]) amplify noise because derivatives enhance high-frequency content.
> - By averaging perpendicular to the gradient direction, Prewitt and Sobel operators average out random noise fluctuations before computing the gradient.
> - **Result:** More robust edge detection with fewer false edge detections due to noise.

---

#### 📊 Diagram / Table (if applicable)

```
  Decomposition (Separability):

  Prewitt Gx = Derivative × Smoothing:
  [-1  0  1]     [-1]              [-1  0  1]
  [-1  0  1]  =  [-1] × [1 1 1] = [-1  0  1]  (uniform avg.)
  [-1  0  1]     [-1]              [-1  0  1]

  Sobel Gx = Derivative × Weighted Smoothing:
  [-1  0  1]     [-1]              [-1  0  1]
  [-2  0  2]  =  [-2] × [1 2 1] = [-2  0  2]  (Gaussian-like)
  [-1  0  1]     [-1]              [-1  0  1]

  Noise Reduction Comparison:
  ┌──────────────────┬────────────────────┬──────────────────┐
  │ Operator         │ Smoothing Filter   │ Noise Robustness │
  ├──────────────────┼────────────────────┼──────────────────┤
  │ Simple diff.     │ None               │ Poor             │
  │ Prewitt          │ [1 1 1] uniform    │ Good             │
  │ Sobel            │ [1 2 1] weighted   │ Better           │
  └──────────────────┴────────────────────┴──────────────────┘

  Effect on noisy edge:
  Noisy Edge:  ... 50 52 48 │ 200 198 202 ...
                            ↑ (edge)
  Simple diff: high response at edge BUT also at noise spikes
  Sobel: averages 3 rows → noise is smoothed, edge is preserved
```

---

#### 💡 Example

> Consider a noisy horizontal edge. Without smoothing, the derivative [−1 0 1] applied to a single row detects the edge but also responds strongly to noise. The Sobel Gx kernel averages 3 rows with weights [1 2 1] before differencing, so if one row has a noise spike (e.g., value 250 instead of 100), the averaged value across 3 rows dilutes this spike to approximately (100+250+100)/4 = 137.5, significantly reducing its impact on the gradient computation.

---

#### 🔚 Conclusion

> Both Prewitt and Sobel operators achieve noise reduction through their inherent design: each kernel is separable into a derivative component (for edge detection) and a smoothing component (for noise reduction). The smoothing is applied perpendicular to the gradient direction. Sobel's weighted average [1 2 1] provides better noise suppression than Prewitt's uniform average [1 1 1] because it approximates a Gaussian weighting. This built-in smoothing makes these operators significantly more robust than simple finite difference operators for edge detection in noisy images.

---

---

## ❓ Question 11: Explain intensity-level slicing. Why is logarithmic (log) transformation used in dynamic range compression?

### ✅ Answer:

#### 📖 Definition / Introduction

**Intensity-level slicing** (grey-level slicing) is an enhancement technique that highlights a specific range of intensity values in an image while either suppressing or preserving the remaining values. The **logarithmic (log) transformation** is used to compress the wide dynamic range of certain types of data into a displayable range, particularly useful for images with large variations in intensity like Fourier spectra and astronomical images.

---

#### 📝 Detailed Explanation

**Key Point 1: Intensity-Level Slicing**

> **Purpose:** To highlight specific features that appear in a particular intensity range while deemphasizing others.
>
> **Two approaches:**
>
> **(a) Without background preservation (binary slicing):**
> - Pixels in the range [A, B] → set to a high value (e.g., 255).
> - All other pixels → set to 0.
> - Result: Binary image showing only the region of interest.
> - Formula: s = L−1 if A ≤ r ≤ B, s = 0 otherwise.
>
> **(b) With background preservation:**
> - Pixels in the range [A, B] → set to a high value (e.g., 255).
> - All other pixels → remain at their original intensity.
> - Result: Highlighted region with background context intact.
> - Formula: s = L−1 if A ≤ r ≤ B, s = r otherwise.
>
> **Applications:**
> - Highlighting water bodies in satellite images.
> - Isolating specific tissue types in medical images.
> - Detecting defects in industrial inspection.

**Key Point 2: Logarithmic Transformation for Dynamic Range Compression**

> The **log transformation** is defined as:
>
> **s = c × log(1 + r)**
>
> where c is a scaling constant and r is the input intensity.
>
> **Why it is used for dynamic range compression:**
>
> 1. **Large dynamic range problem:** Some image data (e.g., Fourier spectrum magnitudes) have values ranging from 0 to millions. Directly displaying this would result in all values appearing as either black (low values are comparatively tiny) or white (high values saturate).
>
> 2. **Logarithmic behaviour:** The log function:
>    - Expands low-intensity values (dark regions → brighter, more distinguishable).
>    - Compresses high-intensity values (bright values → closer together).
>    - Maps the range [0, 10⁶] to approximately [0, 6c] — a manageable range.
>
> 3. **Human perception:** The human eye perceives brightness approximately logarithmically (Weber's law). The log transform aligns the image display with human perception.
>
> 4. **Fourier spectrum display:** |F(u,v)| can range from 0 to millions. Without log: only the DC component (F(0,0)) is visible as a bright dot, everything else appears black. With log: s = c × log(1 + |F|), the spectrum reveals meaningful patterns (edges → directional lines, periodic patterns → dots).

---

#### 📊 Diagram / Table (if applicable)

```
  Intensity-Level Slicing:

  (a) Without background:       (b) With background:
  s ↑                           s ↑
  L ┤       ████                L ┤       ████
    │       ████                  │      ╱████
    │       ████                  │     ╱ ████
    │       ████                  │    ╱  ████╲
  0 ┤───────    ──────          0 ┤───╱       ╲──
    └───┬──A──B──┬──→ r           └───┬──A──B──┬──→ r

  Log Transformation:
  s ↑
    │               ─────────── (compressed high values)
    │           ╱╱
    │        ╱╱
    │     ╱╱
    │  ╱╱                        (expanded low values)
  0 ┤╱
    └──────────────────→ r
    0              10^6
  s = c × log(1 + r)

  Fourier Spectrum Display:
  Without log:                 With log:
  ┌──────────────┐             ┌──────────────┐
  │              │             │   ░░░░░░░    │
  │      ●       │             │  ░░████░░░   │
  │              │             │ ░░██████░░░  │
  │              │             │  ░░████░░░   │
  └──────────────┘             └──────────────┘
  (Only DC visible)            (Full spectrum visible)
```

---

#### 💡 Example

> In a satellite image, water bodies have grey levels in the range [50, 80]. Applying intensity-level slicing with [A, B] = [50, 80] highlights all water bodies in white (255) while keeping the rest (land, vegetation, buildings) as background.
>
> For Fourier spectrum display: An image's |F(u,v)| has DC component = 10⁶ and other values ranging 0 to 1000. Without log: only DC is visible. With s = 30 × log(1 + |F|): DC → 30 × log(10⁶+1) ≈ 415, while a value of 100 → 30 × log(101) ≈ 139. Both are now in a displayable range, revealing the full spectrum structure.

---

#### 🔚 Conclusion

> Intensity-level slicing is a targeted enhancement technique that highlights specific intensity ranges, available with or without background preservation. The logarithmic transformation compresses wide dynamic ranges into displayable ranges by expanding low values and compressing high values. The log transform is essential for visualizing Fourier spectra and other data with extreme dynamic ranges, and its behaviour aligns with human brightness perception, making transformed images more intuitive to interpret.

---

---

## ❓ Question 12: What is image averaging? Discuss histogram characteristics for dark images, bright images, and low-contrast images. (Numerical on histogram equalization)

### ✅ Answer:

#### 📖 Definition / Introduction

**Image averaging** is a noise reduction technique that averages multiple noisy copies of the same scene to obtain a cleaner image. The **histogram** of a digital image reveals key visual characteristics — dark, bright, and low-contrast images each have distinctive histogram shapes. **Histogram equalization** is the standard technique for improving contrast by redistributing intensities.

---

#### 📝 Detailed Explanation

**Key Point 1: Image Averaging**

> If multiple images g₁, g₂, ..., gₖ are captured of the same static scene, each corrupted by independent additive noise:
>
> gᵢ(x,y) = f(x,y) + ηᵢ(x,y)
>
> The **averaged image** is:
>
> **ḡ(x,y) = (1/K) Σ[i=1 to K] gᵢ(x,y)**
>
> **Properties:**
> - E[ḡ(x,y)] = f(x,y) — the expected value equals the original (noise has zero mean).
> - Var[ḡ] = σ²_η / K — variance of noise is **reduced by a factor of K**.
> - **SNR improvement:** SNR increases by √K.
> - As K → ∞, ḡ → f (noise is completely eliminated).
>
> **Limitation:** Requires multiple images of the **same static scene** — not applicable for moving scenes.

**Key Point 2: Histogram Characteristics**

> **(a) Dark Image:**
> - Histogram is **shifted to the left** (concentrated at low intensity values).
> - Most pixels have values near 0 (dark).
> - Few or no pixels at high intensity levels.
>
> **(b) Bright Image:**
> - Histogram is **shifted to the right** (concentrated at high intensity values).
> - Most pixels have values near 255 (bright).
> - Few or no pixels at low intensity levels.
>
> **(c) Low-Contrast Image:**
> - Histogram is **concentrated in a narrow range** (neither fully left nor right, but compressed in the middle or any portion).
> - Small difference between darkest and brightest pixels.
> - Image appears flat, dull, and lacks visual punch.
>
> **(d) High-Contrast Image (ideal):**
> - Histogram **spans the entire range** from 0 to 255.
> - Wide, relatively uniform distribution.
> - Image appears vivid with clear detail differentiation.

**Key Point 3: Numerical — Histogram Equalization**

> **Given:** A 3-bit image (L = 8, levels 0–7), size 64 × 64 = 4096 pixels.
>
> | rₖ | nₖ | p(rₖ) = nₖ/4096 | CDF = Σp | sₖ = round(7 × CDF) |
> |----|------|----------|------|------|
> | 0 | 790 | 0.1929 | 0.1929 | 1 |
> | 1 | 1023 | 0.2498 | 0.4427 | 3 |
> | 2 | 850 | 0.2075 | 0.6502 | 5 |
> | 3 | 656 | 0.1602 | 0.8104 | 6 |
> | 4 | 329 | 0.0803 | 0.8907 | 6 |
> | 5 | 245 | 0.0598 | 0.9505 | 7 |
> | 6 | 122 | 0.0298 | 0.9803 | 7 |
> | 7 | 81 | 0.0198 | 1.0001 | 7 |
>
> **Mapping:** 0→1, 1→3, 2→5, 3→6, 4→6, 5→7, 6→7, 7→7
>
> **Equalized histogram:**
> | sₖ | Pixels |
> |----|--------|
> | 1 | 790 |
> | 3 | 1023 |
> | 5 | 850 |
> | 6 | 656+329 = 985 |
> | 7 | 245+122+81 = 448 |
>
> The equalized histogram is more spread out (levels 1, 3, 5, 6, 7) compared to the original (concentrated at 0–3).

---

#### 📊 Diagram / Table (if applicable)

```
  Image Averaging:
  g₁ = f + η₁ ──┐
  g₂ = f + η₂ ──┼──→ ḡ = (1/K)Σgᵢ ≈ f   (noise ↓ by √K)
  ...            │
  gₖ = f + ηₖ ──┘

  Histogram Characteristics:
  Dark Image:            Bright Image:          Low-Contrast:
  │█                     │              █       │      ██
  │██                    │             ██       │     ████
  │████                  │            ████      │    ██████
  │██████                │          ██████      │   ████████
  └──────────→           └──────────────→       └───────────→
  0     128    255       0     128    255       0    128   255
  (Left-shifted)         (Right-shifted)        (Narrow, middle)

  After Histogram Equalization:
  Original:              Equalized:
  │████                  │ █  █  █  █ █
  │██████                │ █  █  █  █ █
  │████████              │ ██ █  ██ █ █
  └──────────→           └──────────────→
  (Concentrated)         (Spread/uniform)
```

---

#### 💡 Example

> A security camera captures 100 frames of a static lobby. Each frame has Gaussian noise (σ = 20). Averaging all 100 frames reduces noise standard deviation to σ/√100 = 2, producing a nearly noise-free image. The averaged image's histogram is initially concentrated (low contrast). After histogram equalization using the CDF mapping, the histogram spreads across 0–255, producing a vivid, high-contrast result.

---

#### 🔚 Conclusion

> Image averaging reduces noise by a factor of √K when K images of the same scene are averaged, making it effective for static scene noise reduction. Histogram characteristics reveal image quality: dark images have left-shifted histograms, bright images have right-shifted histograms, and low-contrast images have narrow histograms. Histogram equalization transforms the histogram toward a uniform distribution using the CDF as a mapping function, maximizing contrast and improving visual quality.

---

---

## ❓ Question 13: Describe edge detection operators. What is point processing? What are image sharpening filters? What is local enhancement? (Numerical on Arithmetic Mean, Harmonic Mean, Max and Min filters)

### ✅ Answer:

#### 📖 Definition / Introduction

**Edge detection operators** identify boundaries where significant intensity changes occur. **Point processing** transforms each pixel independently. **Sharpening filters** enhance edges and fine details by amplifying high-frequency components. **Local enhancement** applies enhancement operations to local neighbourhoods rather than globally. Several **order-statistic and mean filters** — including arithmetic mean, harmonic mean, max, and min filters — are commonly used for noise reduction.

---

#### 📝 Detailed Explanation

**Key Point 1: Edge Detection Operators**

> Edges are regions of sharp intensity change. Edge detection uses **derivative-based operators**:
>
> **(a) First-order derivative operators (gradient):**
> - **Roberts Cross:** 2×2 kernels, fast but noise-sensitive.
>   - Gx = [1 0; 0 −1], Gy = [0 1; −1 0]
> - **Prewitt:** 3×3, uniform smoothing + differentiation.
>   - Gx = [−1 0 1; −1 0 1; −1 0 1]
> - **Sobel:** 3×3, weighted smoothing + differentiation.
>   - Gx = [−1 0 1; −2 0 2; −1 0 1]
> - **Canny:** Multi-step optimal edge detector (Gaussian smoothing → gradient → non-maximum suppression → hysteresis thresholding).
>
> **(b) Second-order derivative operators:**
> - **Laplacian:** ∇²f = [0 1 0; 1 −4 1; 0 1 0]. Detects edges as zero-crossings.
> - **Laplacian of Gaussian (LoG):** Smooths first, then applies Laplacian.

**Key Point 2: Point Processing**

> **Point processing** transforms each pixel independently without considering its neighbours:
>
> **s = T(r)**
>
> where T depends only on the input pixel value r, not on its location or neighbours.
>
> **Examples:** Negative (s = L−1−r), log transform (s = c·log(1+r)), power-law (s = c·r^γ), thresholding, contrast stretching.

**Key Point 3: Image Sharpening Filters**

> Sharpening filters enhance edges and fine details:
> - **Laplacian:** Second derivative, highlights all edges isotropically.
> - **Unsharp masking:** g = f + k(f − f̄).
> - **High-boost filtering:** g = Af − f̄.
> - **High-pass filtering (frequency domain):** Pass high frequencies, block low frequencies.
> - **Gradient operators:** Sobel, Prewitt for directional sharpening.

**Key Point 4: Local Enhancement**

> **Local enhancement** applies processing based on statistics (mean, variance) computed from a **local neighbourhood** around each pixel, rather than using the global histogram.
>
> At each pixel (x, y), compute local mean mₛ and local variance σₛ² from an n×n neighbourhood. Apply enhancement based on conditions:
>
> If σₛ < k₁·σ_global AND mₛ < k₂·m_global: enhance (multiply by a constant E).
> Otherwise: keep original value.
>
> This allows enhancement of regions with specific local properties (e.g., dark, low-contrast areas) while leaving other regions unchanged.

**Key Point 5: Numerical on Filters**

> Given a 3×3 neighbourhood:
> ```
> ┌─────┬─────┬─────┐
> │  10 │  20 │  30 │
> ├─────┼─────┼─────┤
> │  25 │ 200 │  15 │   ← centre pixel = 200 (possible noise)
> ├─────┼─────┼─────┤
> │  35 │  40 │  45 │
> └─────┴─────┴─────┘
> ```
> Values: {10, 20, 30, 25, 200, 15, 35, 40, 45}
>
> **(a) Arithmetic Mean Filter:**
> f̂ = (1/9)(10+20+30+25+200+15+35+40+45) = 420/9 = **46.67 ≈ 47**
>
> **(b) Harmonic Mean Filter:**
> f̂ = 9 / (1/10 + 1/20 + 1/30 + 1/25 + 1/200 + 1/15 + 1/35 + 1/40 + 1/45)
> = 9 / (0.1 + 0.05 + 0.0333 + 0.04 + 0.005 + 0.0667 + 0.0286 + 0.025 + 0.0222)
> = 9 / 0.3708 = **24.27 ≈ 24**
>
> **(c) Max Filter:**
> f̂ = max{10, 20, 30, 25, 200, 15, 35, 40, 45} = **200**
>
> **(d) Min Filter:**
> f̂ = min{10, 20, 30, 25, 200, 15, 35, 40, 45} = **10**
>
> **Observation:** Arithmetic mean (47) includes noise effect. Harmonic mean (24) is less affected by the outlier 200. Max (200) preserves the noise. Min (10) removes the noise spike entirely.

---

#### 📊 Diagram / Table (if applicable)

```
  Edge Detection Operators:
  ┌──────────┬────────────────────────┬──────────────┐
  │ Operator │ Kernel                 │ Smoothing    │
  ├──────────┼────────────────────────┼──────────────┤
  │ Roberts  │ [1 0; 0 -1]           │ None         │
  │ Prewitt  │ [-1 0 1; -1 0 1; ...] │ Uniform [111]│
  │ Sobel    │ [-1 0 1; -2 0 2; ...] │ Weighted[121]│
  │ Laplacian│ [0 1 0; 1 -4 1; ...]  │ None         │
  │ Canny    │ Multi-step             │ Gaussian     │
  └──────────┴────────────────────────┴──────────────┘

  Filter Comparison for the numerical:
  ┌──────────────────┬────────┬─────────────────────────┐
  │ Filter           │ Output │ Best for                │
  ├──────────────────┼────────┼─────────────────────────┤
  │ Arithmetic Mean  │ 47     │ Gaussian noise           │
  │ Harmonic Mean    │ 24     │ Salt noise (not pepper)  │
  │ Max Filter       │ 200    │ Removing pepper noise    │
  │ Min Filter       │ 10     │ Removing salt noise      │
  │ Median Filter    │ 30     │ Salt-and-pepper noise    │
  └──────────────────┴────────┴─────────────────────────┘
```

---

#### 💡 Example

> In a surveillance image with Gaussian noise, an arithmetic mean filter (3×3) is applied to reduce the overall noise level. For an image with salt noise (random white pixels), the harmonic mean filter is effective because it gives less weight to very large values. The min filter removes salt noise by selecting the smallest value (ignoring the white spikes), while the max filter removes pepper noise by selecting the largest value (ignoring the black dots).

---

#### 🔚 Conclusion

> Edge detection operators use first-order (Sobel, Prewitt) or second-order (Laplacian) derivatives to identify intensity transitions. Point processing transforms pixels independently using transfer functions. Sharpening filters emphasize high-frequency content through derivative-based operations or unsharp masking. Local enhancement adapts processing to neighbourhood statistics for targeted improvement. Different mean and order-statistic filters serve different noise types: arithmetic mean for Gaussian noise, harmonic mean for salt noise, max for pepper noise, min for salt noise, and median for impulse noise.

---

---

## ❓ Question 14: Explain the process of image enhancement using arithmetic operators. What is the need for interpolation techniques? (Numerical on mean and entropy of an image)

### ✅ Answer:

#### 📖 Definition / Introduction

**Arithmetic operators** (addition, subtraction, multiplication, division) are fundamental operations used for image enhancement, noise reduction, change detection, and masking. **Interpolation techniques** are needed when geometric transformations produce pixel locations at non-integer coordinates. **Mean** and **entropy** are statistical measures that characterize the intensity distribution and information content of an image.

---

#### 📝 Detailed Explanation

**Key Point 1: Image Enhancement Using Arithmetic Operators**

> **(a) Addition (Image Averaging):**
> g(x,y) = (1/K) Σ fᵢ(x,y) — averages K noisy images of the same scene.
> - Reduces noise by factor √K.
> - Requires static scene and multiple captures.
>
> **(b) Subtraction (Image Differencing):**
> g(x,y) = f₁(x,y) − f₂(x,y) — highlights differences between two images.
> - Applications: Change detection, motion detection, background subtraction, mask subtraction (digital subtraction angiography).
>
> **(c) Multiplication (Masking/ROI extraction):**
> g(x,y) = f(x,y) × m(x,y) — multiplies image by a mask.
> - If m(x,y) = 1 in ROI and 0 elsewhere: extracts region of interest.
> - If m = constant > 1: brightens the image (scaling).
> - Shading correction: multiply by inverse of illumination pattern.
>
> **(d) Division (Ratio imaging):**
> g(x,y) = f₁(x,y) / f₂(x,y) — ratio of two images.
> - Used in multi-spectral imaging for change detection and normalization.
> - Illumination correction: divide by illumination pattern.

**Key Point 2: Need for Interpolation Techniques**

> Interpolation is needed when:
>
> - **Image resizing** (scaling up/down) — new pixel locations don't align with original grid.
> - **Rotation** — rotated pixel coordinates fall at non-integer positions.
> - **Geometric correction** — correcting lens distortion or perspective.
> - **Image registration** — aligning images from different sources.
> - **Any geometric transformation** maps output pixels to non-integer input locations.
>
> Without interpolation, pixel values at non-integer locations cannot be determined. Common methods: nearest-neighbour, bilinear, bicubic.

**Key Point 3: Numerical — Mean and Entropy**

> **Given image (4×4):**
> ```
> 0  1  2  3
> 4  5  6  7
> 0  2  4  6
> 1  3  5  7
> ```
>
> **Mean:**
> μ = (1/16) × (0+1+2+3+4+5+6+7+0+2+4+6+1+3+5+7)
> μ = (1/16) × 56 = **3.5**
>
> **Entropy (information content):**
> First, compute the histogram (frequency of each value):
> | Value | Count | p(rₖ) = count/16 |
> |-------|-------|----------|
> | 0 | 2 | 0.125 |
> | 1 | 2 | 0.125 |
> | 2 | 2 | 0.125 |
> | 3 | 2 | 0.125 |
> | 4 | 2 | 0.125 |
> | 5 | 2 | 0.125 |
> | 6 | 2 | 0.125 |
> | 7 | 2 | 0.125 |
>
> **H = −Σ p(rₖ) × log₂(p(rₖ))**
> H = −8 × [0.125 × log₂(0.125)]
> H = −8 × [0.125 × (−3)]
> H = −8 × (−0.375)
> H = **3.0 bits/pixel**
>
> Maximum possible entropy for L=8 levels = log₂(8) = 3.0 bits/pixel.
> Since all values are equally probable, entropy is **maximum** — the image has maximum information content.

---

#### 📊 Diagram / Table (if applicable)

```
  Arithmetic Operations for Enhancement:

  Addition (Averaging):          Subtraction (Change Detection):
  f₁ + f₂ + ... + fₖ            f₁(x,y) − f₂(x,y)
  ────────────────── = ḡ          = Difference image
         K                        (highlights changes)

  Multiplication (Masking):      Division (Normalization):
  f(x,y) × m(x,y)               f₁(x,y) / f₂(x,y)
  = ROI extraction               = Ratio image

  Interpolation Need:
  Original grid:    After rotation:
  ● ● ● ● ●        ○ ○ ○ ○ ○    ○ = new pixel positions
  ● ● ● ● ●            ↗            (non-integer in original)
  ● ● ● ● ●        ○ ○ ○ ○ ○    Must interpolate from
  ● ● ● ● ●                      nearest ● values
  ● ● ● ● ●

  Entropy Formula:
  H = −Σ p(rₖ) × log₂(p(rₖ)) bits/pixel
  Max entropy = log₂(L) when all levels equally probable
```

---

#### 💡 Example

> **Digital Subtraction Angiography (DSA):** A pre-contrast X-ray (f₁) is subtracted from a post-contrast X-ray (f₂): g = f₂ − f₁. The difference image shows only the blood vessels filled with contrast agent, removing all background bone and tissue structures.
>
> The computed entropy of 3.0 bits/pixel means the image requires at least 3 bits per pixel for lossless compression (equivalent to 16 × 3 = 48 bits total for this 4×4 image).

---

#### 🔚 Conclusion

> Arithmetic operators (addition, subtraction, multiplication, division) provide fundamental image enhancement capabilities: addition for noise reduction, subtraction for change detection, multiplication for masking, and division for normalization. Interpolation techniques are essential whenever geometric transformations produce non-integer pixel coordinates. Image mean and entropy are key statistical measures — mean indicates average brightness, while entropy (measured in bits/pixel) quantifies the information content and determines the theoretical minimum for lossless compression.

---

---

## ❓ Question 15: Describe the algorithm for image sharpening using DFT and IDFT. Explain the model of the image restoration process in the presence of noise.

### ✅ Answer:

#### 📖 Definition / Introduction

**Image sharpening using DFT/IDFT** is a frequency-domain approach that enhances edges and fine details by applying a **high-pass filter** to the image's frequency representation. The **image restoration model** describes how an original image is degraded by a combination of a degradation function and additive noise, and how restoration attempts to recover the original.

---

#### 📝 Detailed Explanation

**Key Point 1: Image Sharpening Algorithm Using DFT and IDFT**

> **Algorithm:**
>
> **Step 1: Pre-processing**
> - Multiply the input image f(x,y) by (−1)^(x+y) to centre the DFT spectrum.
>
> **Step 2: Forward DFT**
> - Compute the 2D DFT: F(u,v) = DFT{f(x,y) × (−1)^(x+y)}
>
> **Step 3: Design a high-pass filter H(u,v)**
> - Options: Ideal HPF, Butterworth HPF, or Gaussian HPF.
> - Gaussian HPF: H(u,v) = 1 − e^(−D²(u,v)/2D₀²)
> - Where D(u,v) = √(u² + v²) is the distance from the centre.
>
> **Step 4: Apply the filter**
> - G(u,v) = F(u,v) × H(u,v)
>
> **Step 5: Inverse DFT**
> - g'(x,y) = IDFT{G(u,v)}
>
> **Step 6: Post-processing**
> - Multiply by (−1)^(x+y) to undo the centring.
> - Take the real part: g(x,y) = Re{g'(x,y) × (−1)^(x+y)}
>
> The result g(x,y) is a sharpened image with enhanced edges.

**Key Point 2: Image Restoration Model**

> The degradation model in the presence of noise:
>
> **Spatial domain:**
> g(x,y) = h(x,y) ∗ f(x,y) + η(x,y)
>
> **Frequency domain:**
> G(u,v) = H(u,v) · F(u,v) + N(u,v)
>
> Where:
> - **f(x,y)** = original (undegraded) image
> - **h(x,y)** = degradation function (PSF — Point Spread Function)
> - **η(x,y)** = additive noise
> - **g(x,y)** = observed (degraded) image
> - **H(u,v)** = Optical Transfer Function (OTF) = FT{h}
> - **N(u,v)** = noise spectrum
>
> **Restoration goal:** Estimate f̂(x,y) from g(x,y), given knowledge (or estimates) of h and noise statistics.
>
> **Restoration methods:**
> - **Inverse filter:** F̂ = G/H — simple but amplifies noise where H ≈ 0.
> - **Wiener filter:** F̂ = H*G/(|H|²+K) — balances deblurring and noise.
> - **Constrained Least Squares:** Minimizes ||∇²f̂||² subject to ||g − Hf̂||² = ||η||².
> - **Lucy-Richardson:** Iterative algorithm for Poisson noise.

---

#### 📊 Diagram / Table (if applicable)

```
  Sharpening Algorithm (DFT/IDFT):

  f(x,y) → [×(-1)^(x+y)] → [DFT] → F(u,v) → [×H_hp(u,v)] → G(u,v)
                                                                   │
  g(x,y) ← [×(-1)^(x+y)] ← [Real part] ← [IDFT] ←──────────────┘

  High-Pass Filter H(u,v):
  |H|
  1 ┤              ╱──────── (pass high freq.)
    │            ╱
    │          ╱
  0 ┤─────────╱              (block low freq.)
    └────────┬──────→ D(u,v)
             D₀

  Degradation/Restoration Model:

  Original f ──→ [Degradation h] ──→ (+) ──→ Degraded g ──→ [Restoration] ──→ f̂
                                      ↑
                                   Noise η

  In Frequency Domain:
  G(u,v) = H(u,v)·F(u,v) + N(u,v)

  Restoration Attempts:
  ┌──────────────┬──────────────────────────────────┐
  │ Method       │ Formula                          │
  ├──────────────┼──────────────────────────────────┤
  │ Inverse      │ F̂ = G / H                        │
  │ Wiener       │ F̂ = H*G / (|H|² + K)             │
  │ Constrained  │ F̂ = H*G / (|H|² + γ|P|²)        │
  └──────────────┴──────────────────────────────────┘
```

---

#### 💡 Example

> A blurry photograph (degraded by motion blur h and Gaussian noise η) is restored using the Wiener filter. The FFT of the degraded image G(u,v) is computed. The known motion blur PSF H(u,v) and estimated NSR K=0.01 are used. The restored image F̂ = H*G/(|H|²+0.01) recovers significant detail from the blur while keeping noise amplification under control.

---

#### 🔚 Conclusion

> Image sharpening using DFT/IDFT involves transforming to the frequency domain, applying a high-pass filter to enhance edges and details, and transforming back. The image restoration model g = h∗f + η describes how images are degraded by blurring (h) and noise (η). Restoration methods — from simple inverse filtering to the optimal Wiener filter — aim to recover the original image by estimating and reversing the degradation process while controlling noise amplification.

---

---

## ❓ Question 16: Explain the process of image convolution with a suitable example. (Numerical on isotropic filters)

### ✅ Answer:

#### 📖 Definition / Introduction

**Convolution** is a fundamental mathematical operation in image processing that combines an input image with a filter kernel (mask) to produce an output image. It is the basis of all linear spatial filtering operations including smoothing, sharpening, and edge detection. **Isotropic filters** produce the same response regardless of the direction of the features in the image.

---

#### 📝 Detailed Explanation

**Key Point 1: Image Convolution — Process**

> Convolution of an image f(x,y) with a kernel w(s,t) of size m×n is:
>
> **g(x,y) = Σ[s=−a to a] Σ[t=−b to b] w(s,t) · f(x−s, y−t)**
>
> where a = (m−1)/2, b = (n−1)/2.
>
> **Steps:**
> 1. **Flip the kernel** 180° (both horizontally and vertically). For symmetric kernels (most smoothing/Laplacian filters), flipping has no effect.
> 2. **Slide the flipped kernel** across the image, one pixel at a time.
> 3. At each position, **multiply** each kernel element with the corresponding pixel underneath.
> 4. **Sum** all products to get the output pixel value at that position.
> 5. **Handle boundaries:** Pad the image (zero padding, replicate padding, mirror padding).
>
> **Note:** Convolution (flip kernel + slide) vs. Correlation (slide without flip). For symmetric kernels, both give the same result.

**Key Point 2: Convolution Example**

> **Image (5×5):**
> ```
> 0   0   0   0   0
> 0  100 100 100  0
> 0  100 100 100  0
> 0  100 100 100  0
> 0   0   0   0   0
> ```
>
> **Kernel (3×3 averaging):**
> ```
> 1/9  1/9  1/9
> 1/9  1/9  1/9
> 1/9  1/9  1/9
> ```
>
> **Computing g(2,2)** (centre pixel):
> g(2,2) = (1/9)(100+100+100+100+100+100+100+100+100) = 900/9 = **100**
>
> **Computing g(1,1)** (corner of bright region):
> g(1,1) = (1/9)(0+0+0+0+100+100+0+100+100) = 400/9 = **44.4 ≈ 44**
>
> **Computing g(0,0)** (top-left corner, with zero padding):
> g(0,0) = (1/9)(0+0+0+0+0+0+0+0+100) = 100/9 = **11.1 ≈ 11**
>
> The bright square's edges become gradually blurred (intensity transitions are smoothed).

**Key Point 3: Isotropic Filters (Numerical)**

> An **isotropic filter** has the same response in all directions (rotationally symmetric). The Laplacian is the simplest isotropic derivative operator.
>
> **Isotropic Laplacian Kernel (4-neighbour):**
> ```
> [ 0  1  0]
> [ 1 -4  1]
> [ 0  1  0]
> ```
>
> **Isotropic Laplacian Kernel (8-neighbour):**
> ```
> [ 1  1  1]
> [ 1 -8  1]
> [ 1  1  1]
> ```
>
> **Numerical Example — applying 4-neighbour Laplacian:**
>
> Image region:
> ```
> 50   50   50
> 50  100   50
> 50   50   50
> ```
>
> ∇²f(1,1) = 0×50 + 1×50 + 0×50 + 1×50 + (−4)×100 + 1×50 + 0×50 + 1×50 + 0×50
> = 50 + 50 + (−400) + 50 + 50 = **−200**
>
> The large negative value indicates the centre pixel is a **bright spot** (local maximum) surrounded by lower values.
>
> **Isotropic Gaussian smoothing kernel (5×5, σ=1):**
> ```
>     1   4   7   4   1
>     4  16  26  16   4
> 1/  7  26  41  26   7   ×(1/273)
>     4  16  26  16   4
>     1   4   7   4   1
> ```
> This is isotropic because it is circularly symmetric — the response is the same in all directions.

---

#### 📊 Diagram / Table (if applicable)

```
  Convolution Process:

  Step 1: Flip kernel 180°    Step 2: Slide over image
  ┌───────┐   Flip    ┌───────┐    ┌───────────────┐
  │ a b c │  ────→    │ i h g │    │ ● ● ● ● ● ●  │
  │ d e f │           │ f e d │    │ ● ●[×]● ● ●  │ ← kernel position
  │ g h i │           │ c b a │    │ ● ● ● ● ● ●  │
  └───────┘           └───────┘    │ ● ● ● ● ● ●  │
                                   └───────────────┘
  Step 3: Multiply & Sum

  Isotropic Property:
  Isotropic filter produces          Non-isotropic filter:
  circular response:                 directional response:
       ╱ ○ ╲                              ──────
      ○     ○                             ──────
       ╲ ○ ╱                              ──────
  (Same in all directions)           (Stronger in one direction)

  Isotropic Kernels:
  ┌──────────────────┬───────────────────────────────┐
  │ Filter           │ Kernel                        │
  ├──────────────────┼───────────────────────────────┤
  │ Box (averaging)  │ All 1/9 (3×3)                 │
  │ Gaussian         │ Bell-curve weights (symmetric) │
  │ Laplacian (4-N)  │ [0 1 0; 1 -4 1; 0 1 0]       │
  │ Laplacian (8-N)  │ [1 1 1; 1 -8 1; 1 1 1]       │
  └──────────────────┴───────────────────────────────┘
```

---

#### 💡 Example

> A 3×3 Gaussian kernel (isotropic) applied to a photograph smooths it equally in all directions — horizontal, vertical, and diagonal edges are blurred equally. Applying the isotropic 4-neighbour Laplacian to a text image: at the edge of a letter, ∇²f produces a large positive or negative response (highlighting the edge), while in flat regions ∇²f ≈ 0 (no response). The isotropy ensures edges in all orientations are detected equally.

---

#### 🔚 Conclusion

> Image convolution is the core operation of spatial filtering — it slides a flipped kernel across the image, computing weighted sums at each position. The process handles boundary pixels through padding. Isotropic filters like the Laplacian and Gaussian produce direction-independent responses, making them fundamental to smoothing (Gaussian) and edge detection (Laplacian). Understanding convolution — both its mathematical definition and practical computation — is essential for all spatial-domain image processing operations.

---

---

> 💡 *More questions will be added as provided by Rishav.*

---

*📑 Documented by Rishav | Wishing you all the very best in your upcoming examinations! 🌟🎓*
