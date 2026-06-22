

# 📘 B.Tech 6th Semester — Exam Preparation

**Author:** Rishav Raj | **Semester:** 6th Sem | **Subject:** Image Processing — Image Restoration | **Marks per Answer:** 5–10 Marks

--- 

## 📌 How to Use This Document

- Each answer is structured for **5–10 marks** university exam questions.
- Every answer covers **1-2 pages** of content with proper depth.
- Format includes: **Definition → Explanation → Key Points → Diagram/Example → Conclusion**

---

---

## ❓ Question 1: List the various geometric transformations. Differentiate between unconstrained restoration and constrained restoration. Briefly explain the region growing technique and state its problems. What are linear and non-linear geometric image transformations? Differentiate between them.

### ✅ Answer:

#### 📖 Definition / Introduction

**Geometric transformations** modify the spatial relationships between pixels in an image (e.g., scaling, rotation). They are divided into **linear** (preserving straight lines) and **non-linear** (warping) transformations. **Image restoration** can be **unconstrained** (minimizing error without prior knowledge) or **constrained** (incorporating prior knowledge like smoothness). **Region growing** is a segmentation technique that groups pixels into larger regions based on predefined similarity criteria.

---

#### 📝 Detailed Explanation

**Key Point 1: Various Geometric Transformations & Linear vs Non-Linear**

> **Geometric transformations** change the spatial layout of an image (coordinate transformations).
>
> **Linear Transformations (Affine Transformations):**
> Preserve collinearity (points on a line remain on a line) and ratios of distances.
> - **Translation:** Shifting the image along x and/or y axes.
> - **Scaling:** Resizing the image (enlarging or shrinking).
> - **Rotation:** Turning the image around a pivot point.
> - **Shearing:** Slanting the image along an axis.
>
> **Non-Linear Transformations:**
> Do not preserve straight lines; they cause local warping or distortion.
> - **Perspective Projection:** Simulates viewing a 3D plane from an angle.
> - **Polynomial Warping:** Used for correcting lens distortions (barrel/pincushion).
> - **Rubber-sheet mapping:** Correcting complex spatial distortions by tying specific points to new coordinates.
>
> | Feature | Linear Transformations | Non-Linear Transformations |
> |---------|------------------------|----------------------------|
> | **Line Preservation** | Straight lines remain straight | Straight lines may become curved |
> | **Matrix Representation** | Can be represented by a single 3x3 matrix (affine) | Requires polynomial or complex equations |
> | **Complexity** | Computationally simple | Computationally intensive |
> | **Applications** | Standard resizing, rotation, translation | Lens distortion correction, morphing, perspective correction |

**Key Point 2: Unconstrained vs. Constrained Restoration**

> Image restoration aims to recover the original image from a degraded version.
>
> **Unconstrained Restoration:**
> Minimizes a criterion function (usually least squares error) without adding any constraints about the image's characteristics.
> - **Method:** Minimizes the error between the observed image and the degraded estimate.
> - **Result:** Leads to the **Inverse Filter**.
> - **Drawback:** Highly sensitive to noise. If the degradation function has values close to zero, noise is amplified drastically, which can ruin the restored image.
>
> **Constrained Restoration:**
> Incorporates prior knowledge about the image (e.g., images are generally smooth) by adding mathematical constraints to the minimization problem.
> - **Method:** Minimizes a function (like the Laplacian, measuring roughness) subject to the constraint that the residual error equals the noise variance.
> - **Result:** Leads to the **Constrained Least Squares Filter** or **Wiener Filter**.
> - **Advantage:** Much more stable in the presence of noise, producing visually superior results compared to unconstrained methods.

**Key Point 3: Region Growing Technique and Its Problems**

> **Region Growing** is a bottom-up image segmentation method.
>
> **Algorithm:**
> 1. Select a set of **seed points** (pixels) based on some criteria (e.g., highest intensity).
> 2. Check neighboring pixels (4-connected or 8-connected).
> 3. If a neighbor meets a **similarity criterion** (e.g., intensity difference < threshold), append it to the seed's region.
> 4. The new pixel acts as a new seed. Repeat until no more pixels can be added.
>
> **Problems / Limitations:**
> - **Seed Selection:** The final segmentation heavily depends on the initial choice of seed points. Poor seed selection leads to incorrect segmentation.
> - **Stopping Criteria:** Difficult to formulate robust rules for when to stop growing.
> - **Noise Sensitivity:** Random noise can prematurely stop region growing or erroneously connect two regions that should be separate (leakage).
> - **Computationally Intensive:** Requires checking many local neighborhoods iteratively, which can be slow for large images.

---

#### 📊 Diagram / Table (if applicable)

```
  Restoration Approaches:
  
  Unconstrained: Minimize ||g - Hf||²  →  Sensitive to noise (Inverse Filter)
  Constrained:   Minimize ||Qf||² subject to ||g - Hf||² = ||n||² → Robust (Wiener/CLS)

  Region Growing Process:
  [S] = Seed pixel
  [ ] = Unassigned pixel
  [R] = Region pixel

  Step 1:       Step 2:       Step 3:
  [ ][ ][ ]     [ ][R][ ]     [R][R][R]
  [ ][S][ ]  →  [R][S][R]  →  [R][S][R]
  [ ][ ][ ]     [ ][R][ ]     [R][R][R]
  (Checks neighbors based on similarity to grow region)
```

---

#### 💡 Example

> If a document image is photographed at an angle, a **perspective (non-linear) transformation** corrects the keystoning effect so the page looks flat. If an image is blurry, an **unconstrained inverse filter** might amplify sensor noise to the point where the text is illegible, whereas a **constrained least squares filter** will restore the text edges while keeping noise suppressed. To extract the text from the background, **region growing** could start at dark seed points (ink) and grow to cover whole characters.

---

#### 🔚 Conclusion

> Geometric transformations adjust spatial coordinates, with linear methods preserving lines and non-linear methods enabling complex warping. In restoration, constrained methods significantly outperform unconstrained methods by incorporating prior knowledge to prevent noise amplification that plagues inverse filtering. Region growing is a classic segmentation approach that builds regions from seed points but struggles with noise and seed selection sensitivity.

---

---

## ❓ Question 2: Explain the image restoration model. Explain the restoration model for a continuous function in detail. Describe the image degradation model.

### ✅ Answer:

#### 📖 Definition / Introduction

The **image degradation/restoration model** mathematically describes how an original image is corrupted by a physical degradation process and additive noise, and how a restoration process attempts to estimate the original image. Understanding both the discrete and **continuous function** forms of this model is fundamental to developing effective restoration filters that reverse the blur and suppress noise.

---

#### 📝 Detailed Explanation

**Key Point 1: Image Degradation Model**

> The degradation process models how physical phenomena (like motion blur, out-of-focus lenses, or atmospheric turbulence) and sensor noise corrupt an ideal image.
>
> Let:
> - **f(x, y)** = Original, ideal image
> - **h(x, y)** = Degradation function (also known as the Point Spread Function, PSF)
> - **η(x, y)** = Additive noise (from sensors, transmission, etc.)
> - **g(x, y)** = Observed, degraded image
>
> **The Model Equation (Spatial Domain):**
> **g(x, y) = h(x, y) ∗ f(x, y) + η(x, y)**
> *(where ∗ denotes spatial convolution)*
>
> **The Model Equation (Frequency Domain):**
> Using the convolution theorem, we transform the model into the frequency domain:
> **G(u, v) = H(u, v) · F(u, v) + N(u, v)**
>
> The goal of restoration is to obtain an estimate, **f̂(x, y)**, of the original image f(x, y), such that f̂(x, y) is as close as possible to f(x, y).

**Key Point 2: Restoration Model for a Continuous Function**

> While digital images are discrete, the underlying physical degradation process is continuous.
>
> Let f(α, β) be a continuous, 2D object space (the real world).
> Let g(x, y) be the continuous image plane.
>
> The degradation function **h(x, y, α, β)** represents the response of the imaging system at image coordinates (x, y) to a point source located at (α, β) in the object plane.
>
> **General Continuous Degradation Model:**
> **g(x, y) = ∫∫ f(α, β) · h(x, y, α, β) dα dβ + η(x, y)**
> *(Limits of integration are over the entire object space)*
>
> **Position Invariant (Shift Invariant) Assumption:**
> In most practical applications, we assume the degradation is **position invariant**. This means the system's response to a point source only depends on the *distance* between the source and the observation point, not on their absolute positions.
>
> Mathematically, h(x, y, α, β) becomes **h(x - α, y - β)**.
>
> Substituting this back into the integral yields the **continuous convolution integral**:
> **g(x, y) = ∫∫ f(α, β) · h(x - α, y - β) dα dβ + η(x, y)**
>
> This continuous convolution is what we sample to obtain the discrete convolution model g(x,y) = h(x,y) ∗ f(x,y) + η(x,y).

**Key Point 3: The Image Restoration Process**

> The restoration process involves reversing the degradation. Since we only have G(u,v), and we usually know or can estimate H(u,v) and N(u,v), we apply a restoration filter.
>
> **1. Estimation of Degradation (H):** By observation, experimentation (using a point light source to find the PSF), or mathematical modeling (e.g., modeling motion blur).
> **2. Estimation of Noise (N):** By analyzing uniform/flat regions of the degraded image to find noise variance.
> **3. Application of Filter:** Applying a mathematical filter (Inverse, Wiener, Constrained Least Squares) to compute F̂(u,v).
> **4. Inverse Transform:** Converting F̂(u,v) back to the spatial domain to get f̂(x,y).

---

#### 📊 Diagram / Table (if applicable)

```
  Block Diagram of the Degradation / Restoration Process:

                 Degradation Function h(x,y)
                      [System H]
                           │
  Original Image  ───────→ │ ───────→ + ───────→ Degraded Image
      f(x,y)                          │              g(x,y)
                                      ↑
                                 Noise η(x,y)
                                      │
                                      ▼
                               [Restoration]
                                 [Filter]
                                      │
                                      ▼
                                Estimated Image
                                    f̂(x,y)
```

---

#### 💡 Example

> Consider taking a photograph of a fast-moving car. The original scene is f(x,y). During the exposure time, the car moves, acting as a continuous degradation function h(x,y) (motion blur). The camera sensor also adds random continuous noise η(x,y). The resulting continuous signal is sampled by the camera's pixels to form the discrete degraded image g(x,y). To restore the image, an algorithm estimates the blur direction and length to model H(u,v), and applies a Wiener filter to recover the car's license plate f̂(x,y).

---

#### 🔚 Conclusion

> The image degradation model elegantly represents physical corruption as a combination of convolution with a Point Spread Function and additive noise. The continuous model uses integral calculus to describe the precise optical physics, which simplifies to the convolution integral under the assumption of position invariance. The restoration process uses this model to mathematically estimate the original, undegraded image from the corrupted observation using frequency-domain filtering techniques.

---

---

## ❓ Question 3: What is threshold coding implementation? What is least-square restoration and constrained least-square restoration? Differentiate between them.

### ✅ Answer:

#### 📖 Definition / Introduction

**Threshold coding** is an image compression technique that discards transform coefficients below a certain magnitude to save space. **Least-square restoration** (unconstrained) and **constrained least-square restoration** are mathematical approaches to recovering a degraded image by minimizing an error function. The constrained version incorporates prior knowledge to handle noise much more effectively.

---

#### 📝 Detailed Explanation

**Key Point 1: Threshold Coding Implementation**

> **Threshold coding** is a technique commonly used in transform-based image compression (like DCT in JPEG).
>
> **Process:**
> 1. Transform the image into the frequency domain (e.g., via Discrete Cosine Transform).
> 2. Energy Compaction ensures that most visual information is packed into a few coefficients, while many high-frequency coefficients are near zero.
> 3. **Thresholding:** A threshold value 'T' is chosen. Any coefficient with an absolute magnitude less than 'T' is set to zero.
> 4. The remaining non-zero coefficients are quantized and encoded.
>
> **Result:** Significant compression is achieved because long runs of zeros can be highly compressed (using Run-Length Encoding). It is a **lossy** compression method, as the discarded small coefficients cannot be recovered perfectly.

**Key Point 2: Least-Square Restoration (Unconstrained)**

> This is a restoration method that aims to find an estimate f̂ that minimizes the sum of squared errors between the observed degraded image 'g' and the estimated degraded image 'Hf̂'.
>
> **Objective:** Minimize the error criterion: **J(f̂) = ||g - Hf̂||²**
>
> Taking the derivative and setting it to zero yields the unconstrained least-squares estimate, which mathematically evaluates to the **Inverse Filter**:
> **F̂(u,v) = G(u,v) / H(u,v)**
>
> **Problem:** It completely ignores the presence of noise. Since G = HF + N, the estimate becomes:
> **F̂ = F + N/H**
> If the degradation function H(u,v) has very small values (which is typical for high frequencies), the term N/H becomes massive, **drastically amplifying noise** and ruining the restored image.

**Key Point 3: Constrained Least-Square Restoration**

> To solve the noise amplification problem, this method adds a **constraint** based on prior knowledge — specifically, that natural images are generally smooth.
>
> **Objective:** Minimize a measure of roughness (usually the Laplacian, denoted by operator Q or P).
> Minimize: **||Qf̂||²**
> Subject to the constraint: **||g - Hf̂||² = ||η||²** (The residual error should equal the known noise variance).
>
> Using Lagrange multipliers, this minimization leads to the **Constrained Least Squares Filter**:
>
> **F̂(u,v) = [ H*(u,v) / (|H(u,v)|² + γ|P(u,v)|²) ] · G(u,v)**
>
> Where:
> - P(u,v) is the Fourier transform of the Laplacian operator.
> - γ (gamma) is a parameter adjusted iteratively to satisfy the noise constraint.

**Key Point 4: Differentiation**

> | Feature | Least-Square (Unconstrained) | Constrained Least-Square |
> |---------|------------------------------|--------------------------|
> | **Objective Function** | Minimizes only the data error ||g - Hf̂||² | Minimizes roughness ||Qf̂||² with constraints |
> | **Prior Knowledge** | None | Assumes image is generally smooth |
> | **Resulting Filter** | Inverse Filter | Constrained Least Squares Filter |
> | **Noise Handling** | Extremely poor (amplifies noise massively) | Excellent (balances smoothing and restoration) |
> | **Requirements** | Only needs degradation H | Needs degradation H, noise variance, and an iterative process to find γ |

---

#### 📊 Diagram / Table (if applicable)

```
  Threshold Coding in DCT:
  Before Thresholding: [150, 45, -12, 5, 2, -1, 0, ...]
  Threshold T = 10
  After Thresholding:  [150, 45, -12, 0, 0,  0, 0, ...]
  (Zeros are easily compressed)

  Restoration Filter Shapes:
  Inverse Filter (Unconstrained): 
  Multiplier = 1/H(u,v). Approaches infinity when H approaches zero.
  
  Constrained Least Squares:
  Multiplier = H* / (|H|² + γ|P|²). 
  When H approaches zero, the denominator is bounded by γ|P|², preventing infinity and noise explosion.
```

---

#### 💡 Example

> When compressing a satellite image to send over a slow connection, **threshold coding** discards minor high-frequency details (setting small DCT coefficients to zero), allowing a 10MB image to be transmitted as 1MB with little visible loss.
> If this image was taken out of focus, using **unconstrained least-squares** would result in a screen full of static (noise amplification). Using **constrained least-squares**, the algorithm minimizes the Laplacian (keeping the image looking natural and smooth) while enforcing the blur model, successfully revealing the ground details without noise explosion.

---

#### 🔚 Conclusion

> Threshold coding provides efficient lossy image compression by aggressively discarding low-magnitude transform coefficients. In image restoration, the unconstrained least-squares approach fails practically due to massive noise amplification at frequencies where the degradation function is close to zero. The constrained least-squares restoration solves this by incorporating the mathematical constraint of image smoothness (minimizing the Laplacian), resulting in a stable, optimal restoration that gracefully handles both blur and noise.

---

---

## ❓ Question 4: Describe the restoration technique using homomorphic filtering.

### ✅ Answer:

#### 📖 Definition / Introduction

**Homomorphic filtering** is a technique primarily used to handle image degradations that are **multiplicative** rather than additive. By applying a logarithmic transformation, the multiplicative components are converted into additive components, allowing standard linear filtering techniques (in the frequency domain) to be used for restoration or enhancement, after which an exponential transformation restores the image space.

---

#### 📝 Detailed Explanation

**Key Point 1: The Multiplicative Degradation Model**

> Standard image restoration techniques (like Inverse or Wiener filtering) assume the degradation and noise are *additive*: g = h ∗ f + η.
>
> However, some degradations are **multiplicative**. The most classic example is the **Illumination-Reflectance model** of image formation, but it also applies to **multiplicative noise** (like speckle noise in ultrasound or radar images).
>
> Let the observed degraded image be modeled as:
> **f(x, y) = i(x, y) × r(x, y)**
>
> Where:
> - **i(x, y)** is the illumination component (or multiplicative degradation). It generally varies slowly across the image, meaning it is characterized by **low frequencies**.
> - **r(x, y)** is the reflectance component (the actual object details we want to see). It varies rapidly across the image, characterized by **high frequencies**.
>
> Because they are multiplied together, we cannot simply use a linear high-pass or low-pass filter to separate them directly.

**Key Point 2: The Homomorphic Filtering Process**

> Homomorphic filtering solves the multiplication problem by using the properties of logarithms to convert multiplication into addition.
>
> **Step 1: Logarithmic Transformation**
> Take the natural logarithm of the image to convert multiplication into addition.
> z(x, y) = ln[f(x, y)] = ln[i(x, y) × r(x, y)]
> **z(x, y) = ln[i(x, y)] + ln[r(x, y)]**
> Now, the low-frequency illumination and high-frequency reflectance are additive.
>
> **Step 2: Fourier Transform**
> Convert the log-image into the frequency domain.
> **Z(u, v) = F_i(u, v) + F_r(u, v)**
>
> **Step 3: Linear Filtering in Frequency Domain**
> Apply a carefully designed filter **H(u, v)**. We want to suppress the low-frequency illumination (to correct uneven lighting) and boost the high-frequency reflectance (to enhance details).
> S(u, v) = H(u, v) · Z(u, v)
> **S(u, v) = H(u, v) · F_i(u, v) + H(u, v) · F_r(u, v)**
>
> *Filter Design:* H(u,v) is designed to have a value < 1 for low frequencies (attenuation) and > 1 for high frequencies (amplification).
>
> **Step 4: Inverse Fourier Transform**
> Convert back to the spatial domain.
> **s(x, y) = IDFT{S(u, v)}**
>
> **Step 5: Exponential Transformation**
> Take the exponential to reverse the logarithm applied in Step 1 and obtain the final restored image.
> **g(x, y) = exp[s(x, y)]**

**Key Point 3: Applications as a Restoration Technique**

> While often classed under enhancement (dynamic range compression and contrast enhancement), homomorphic filtering acts as a true restoration technique when the goal is to remove a specific multiplicative corruption:
>
> - **Correcting Uneven Illumination:** Restoring images taken under terrible lighting conditions (e.g., a face half in deep shadow, half in bright sunlight).
> - **Speckle Noise Reduction:** In Synthetic Aperture Radar (SAR) or medical ultrasound, speckle noise is multiplicative. Homomorphic filtering can convert it to additive noise, filter it out, and convert it back to restore the image details.

---

#### 📊 Diagram / Table (if applicable)

```
  Block Diagram of Homomorphic Filtering:

  Multiplicative             Additive                 Additive
     Input      [ Natural ]   Input      [ Fourier ] Frequency  [ Filter ]
  f(x,y)=i×r  → [Logarithm] → z = In(i)+In(r) → [Transform] →   Z(u,v)   → [ H(u,v) ]
                                                                                │
                                                                                │
  Restored                     Additive                 Filtered Additive       ▼
   Image        [Exponential]   Output   [ Inverse ]     Frequency           S(u,v)
   g(x,y)     ← [   exp()   ] ← s(x,y) ← [ Fourier ] ←──────────────────────────┘
```

---

#### 💡 Example

> A radiologist is examining an X-ray where the lighting source was faulty, resulting in the left side of the film being brightly blown out and the right side being completely dark (a multiplicative low-frequency degradation). By applying homomorphic filtering, the algorithm takes the log of the image, applies a filter that heavily attenuates the low frequencies (removing the bright-to-dark gradient), and takes the exponential. The restored image now has perfectly uniform lighting across the whole X-ray, revealing previously hidden bone fractures.

---

#### 🔚 Conclusion

> Homomorphic filtering is a powerful restoration and enhancement technique specifically designed for multiplicative image models, such as illumination-reflectance or speckle noise. By mapping the image into the log domain, it elegantly converts multiplicative components into additive ones, allowing standard frequency-domain filters to suppress illumination variations and amplify structural details simultaneously, before returning the image to the spatial domain via an exponential function.

---

---

> 💡 *More questions will be added as provided by Rishav.*

---

*📑 Documented by Rishav | Wishing you all the very best in your upcoming examinations! 🌟🎓*
