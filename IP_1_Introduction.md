

# 📘 B.Tech 6th Semester — Exam Preparation

**Author:** Rishav Raj | **Semester:** 6th Sem | **Subject:** Image Processing — Introduction | **Marks per Answer:** 5–10 Marks

---

## 📌 How to Use This Document

- Each answer is structured for **5–10 marks** university exam questions.

- Every answer covers **1-2 pages** of content with proper depth.

- Format includes: **Definition → Explanation → Key Points → Diagram/Example → Conclusion**

---

---

## ❓ Question 1: Develop a procedure for computing the median of an n × n neighbourhood. Propose a technique for updating the median as the centre of the neighbourhood is moved from pixel to pixel.

### ✅ Answer:

#### 📖 Definition / Introduction

The **median filter** is a non-linear spatial filtering technique used in image processing to reduce noise (especially salt-and-pepper noise) while preserving edges. Unlike the mean filter, the median filter replaces each pixel's value with the **median** of its n × n neighbourhood. Computing and efficiently updating this median as the filter window slides across the image is a key algorithmic challenge.

---

#### 📝 Detailed Explanation

**Key Point 1: Procedure for Computing the Median of an n × n Neighbourhood**

> **Step 1:** Define the neighbourhood window of size n × n centred at pixel (x, y).
>
> **Step 2:** Extract all n² pixel intensity values from the neighbourhood.
>
> **Step 3:** Sort these n² values in ascending (or descending) order.
>
> **Step 4:** Select the middle value from the sorted list. For n² values (which is always odd when n is odd), the median is the value at position (n² + 1)/2.
>
> **Step 5:** Replace the centre pixel (x, y) with this median value.
>
> **Example:** For a 3 × 3 neighbourhood with values {15, 20, 22, 18, 200, 19, 21, 17, 23}, sorted = {15, 17, 18, 19, 20, 21, 22, 23, 200}, median = 20 (5th value).

**Key Point 2: Technique for Updating the Median (Sliding Window / Huang's Algorithm)**

> When the centre of the neighbourhood moves from pixel (x, y) to (x, y+1) (one column to the right), the n × n window shifts by one column. This means:
>
> - **One column of n pixels is removed** (the leftmost column of the old window).
> - **One column of n pixels is added** (the rightmost column of the new window).
>
> Instead of re-sorting all n² pixels, we use a **histogram-based approach**:
>
> **Step 1:** Maintain a running histogram H of pixel intensities in the current n × n window, along with a count of pixels less than or equal to the current median (called `ltmdn`).
>
> **Step 2:** When the window moves right by one pixel:
> - **Subtract** the n pixels of the outgoing (leftmost) column from H. For each removed pixel value v, if v ≤ current median, decrement `ltmdn`.
> - **Add** the n pixels of the incoming (rightmost) column to H. For each added pixel value v, if v ≤ current median, increment `ltmdn`.
>
> **Step 3:** The median position is at th = (n² + 1)/2.
> - If `ltmdn` ≥ th, the new median may have shifted lower — scan H downward from the current median until `ltmdn` < th.
> - If `ltmdn` < th, the new median may have shifted higher — scan H upward until `ltmdn` ≥ th.
>
> This reduces the complexity from **O(n² log n²)** per pixel (full sort) to approximately **O(n)** per pixel (only updating 2n values and scanning the histogram).

**Key Point 3: Advantages of the Update Technique**

> - **Efficiency:** Only 2n pixels change per move, not all n².
> - **Speed:** The histogram update is O(n), and the median search is O(number of grey levels), making it much faster than re-sorting.
> - **Scalability:** Particularly beneficial for larger window sizes.

---

#### 📊 Diagram / Table (if applicable)

```
  Moving Window (3×3 example, moving right):

  Old Window (at x,y)          New Window (at x, y+1)
  ┌─────┬─────┬─────┐         ┌─────┬─────┬─────┐
  │ a1  │ a2  │ a3  │         │ a2  │ a3  │ b1  │
  ├─────┼─────┼─────┤   →     ├─────┼─────┼─────┤
  │ a4  │ a5  │ a6  │         │ a5  │ a6  │ b2  │
  ├─────┼─────┼─────┤         ├─────┼─────┼─────┤
  │ a7  │ a8  │ a9  │         │ a8  │ a9  │ b3  │
  └─────┴─────┴─────┘         └─────┴─────┴─────┘

  Removed: a1, a4, a7 (left column)
  Added:   b1, b2, b3 (right column)

  Histogram Update:
  H[a1]--, H[a4]--, H[a7]--   (decrement removed)
  H[b1]++, H[b2]++, H[b3]++   (increment added)
  Then adjust median pointer in histogram.
```

---

#### 💡 Example

> Consider a 3 × 3 window scanning a row of a 256-grey-level image. At position (5, 5), the sorted neighbourhood is {10, 12, 14, 15, 18, 20, 22, 25, 30}, median = 18. Moving to (5, 6), pixels {10, 15, 25} are removed and {11, 19, 28} are added. Histogram is updated by decrementing bins 10, 15, 25 and incrementing bins 11, 19, 28. The count `ltmdn` is adjusted, and the histogram is scanned to find the new median = 19.

---

#### 🔚 Conclusion

> The median filter is a powerful tool for noise removal in images, especially salt-and-pepper noise. The naive approach of sorting all n² pixels for every pixel position is computationally expensive. By using a histogram-based sliding window technique (Huang's algorithm), we can efficiently update the median with only O(n) operations per pixel move, making real-time median filtering practical even for large neighbourhood sizes.

---

---

## ❓ Question 2: What is a pixel? Explain 4-neighbour and 8-neighbour of a pixel. Explain m-adjacency.

### ✅ Answer:

#### 📖 Definition / Introduction

A **pixel** (short for "picture element") is the smallest addressable element in a digital image. It represents a single point in a raster image and holds a numerical value corresponding to the intensity or colour at that spatial location. Pixels are arranged in a 2D grid (rows and columns), and their spatial relationships — defined through neighbourhoods and adjacency — are fundamental to image processing operations like segmentation, edge detection, and region analysis.

---

#### 📝 Detailed Explanation

**Key Point 1: Pixel**

> A pixel at coordinates (x, y) in a digital image f has an intensity value f(x, y). For a greyscale image, this value typically ranges from 0 (black) to 255 (white) for an 8-bit image. For a colour image, each pixel stores multiple values (e.g., R, G, B channels). The pixel is the fundamental building block of any digital image and determines its spatial resolution.

**Key Point 2: 4-Neighbour (N₄) of a Pixel**

> The **4-neighbours** of a pixel p at (x, y) are the four pixels that share a horizontal or vertical edge with p. They are located at:
>
> - (x+1, y), (x−1, y), (x, y+1), (x, y−1)
>
> These are also called the **direct neighbours** or **Von Neumann neighbourhood**. The set of these four pixels is denoted as **N₄(p)**. Note: Some of these neighbours may lie outside the image boundary for edge/corner pixels.

**Key Point 3: 8-Neighbour (N₈) of a Pixel**

> The **8-neighbours** of a pixel p at (x, y) include all pixels surrounding p — the 4 direct neighbours plus the 4 diagonal neighbours. They are:
>
> - (x+1, y), (x−1, y), (x, y+1), (x, y−1) — direct neighbours
> - (x+1, y+1), (x+1, y−1), (x−1, y+1), (x−1, y−1) — diagonal neighbours (Nᴅ)
>
> This is also called the **Moore neighbourhood**. N₈(p) = N₄(p) ∪ Nᴅ(p).

**Key Point 4: m-Adjacency (Mixed Adjacency)**

> **m-adjacency** (mixed adjacency) is introduced to eliminate the **ambiguity** that arises with 8-adjacency. Two pixels p and q with values from a set V are **m-adjacent** if:
>
> **(i)** q is in N₄(p) (they are 4-adjacent), **OR**
>
> **(ii)** q is in Nᴅ(p) (they are diagonally adjacent) **AND** the set N₄(p) ∩ N₄(q) has **no pixels with values from V**.
>
> This means: diagonal adjacency is allowed only when there is no 4-connected path between the two pixels through V-valued pixels. This prevents the formation of ambiguous multiple paths between pixels.

---

#### 📊 Diagram / Table (if applicable)

```
   4-Neighbours of p(x,y):          8-Neighbours of p(x,y):

        (x-1,y)                  (x-1,y-1) (x-1,y) (x-1,y+1)
          |                          \       |       /
   (x,y-1)—p(x,y)—(x,y+1)    (x,y-1) — p(x,y) — (x,y+1)
          |                          /       |       \
        (x+1,y)                  (x+1,y-1) (x+1,y) (x+1,y+1)


   m-Adjacency Example:
   ┌───┬───┬───┐     V = {1}
   │ 0 │ 1 │ 0 │     
   ├───┼───┼───┤     p = (1,0), q = (0,1), r = (1,1)
   │ 1 │ 1 │ 0 │     
   ├───┼───┼───┤     8-adjacency: p-q, p-r, q-r (ambiguous path)
   │ 0 │ 0 │ 0 │     m-adjacency: p-r, q-r only (no p-q diagonal
   └───┴───┴───┘     since N₄(p)∩N₄(q) contains r which ∈ V)
```

---

#### 💡 Example

> Consider a binary image region where pixels with value 1 are of interest (V = {1}). If three pixels p(1,0)=1, q(0,1)=1, r(1,1)=1 are present, using 8-adjacency all three are mutually adjacent, creating an ambiguous triangular path. Using m-adjacency, p and q are NOT m-adjacent because their common 4-neighbour r has a value in V. This eliminates the ambiguity and produces a clean single-pixel-wide path: p→r→q.

---

#### 🔚 Conclusion

> A pixel is the fundamental unit of a digital image. The 4-neighbourhood and 8-neighbourhood define the spatial relationship between pixels, which is essential for operations like connectivity analysis and region growing. m-adjacency resolves the ambiguity problem of 8-adjacency by restricting diagonal connections, ensuring unique paths between pixels and making algorithms more deterministic and reliable.

---

---

## ❓ Question 3: Explain image sensing and acquisition using Single Sensor, Sensor Strip, Sensor Array. What are image sensors and how are they used? Discuss one technique of image acquisition.

### ✅ Answer:

#### 📖 Definition / Introduction

**Image sensing and acquisition** is the process of converting a physical scene (continuous visual information) into a digital image that can be processed by a computer. This involves two main elements: a **physical device (sensor)** that is sensitive to electromagnetic energy (such as light), and a **digitizer** that converts the sensor output into a digital form. The type and arrangement of sensors determine the method and quality of image acquisition.

---

#### 📝 Detailed Explanation

**Key Point 1: What are Image Sensors?**

> An **image sensor** is a device that detects and converts incoming electromagnetic energy (visible light, X-rays, infrared, etc.) into an electrical signal. The most common image sensors are:
> - **CCD (Charge-Coupled Device):** Converts photons to electric charge, which is then read out sequentially.
> - **CMOS (Complementary Metal-Oxide-Semiconductor):** Each pixel has its own charge-to-voltage conversion circuit, allowing faster readout.
> - **Photodiodes:** Simple semiconductor devices that produce a voltage proportional to light intensity.

**Key Point 2: Single Sensor Acquisition**

> A **single sensor** (e.g., a single photodiode) captures one pixel's worth of information at a time. To generate a 2D image, the sensor or the object must be mechanically moved in both X and Y directions. This is the slowest method but is used in applications where very high precision is needed.
>
> **Example:** A flatbed scanner uses a single sensor (or a small sensor array acting as one) that is moved across the document line by line.

**Key Point 3: Sensor Strip Acquisition**

> A **sensor strip** is a linear array of sensors arranged in a row. It captures an entire line of the image at once. To form a 2D image, the strip moves perpendicular to its length (or the object moves past the strip), capturing the image one row at a time. This is faster than a single sensor.
>
> **Example:** A flat-bed scanner typically uses a 1D CCD sensor strip that sweeps across the page. Satellite imaging systems like pushbroom scanners use linear sensor arrays — the satellite's orbital motion provides the second dimension.

**Key Point 4: Sensor Array Acquisition**

> A **sensor array** is a 2D grid of sensors (rows × columns) that captures the entire image in a single exposure. This is the fastest method and is used in most modern cameras and imaging devices.
>
> **Example:** A digital camera uses a 2D CCD or CMOS sensor array (e.g., 4000 × 3000 pixels) to capture the full image at once. Each sensor element in the array corresponds to one pixel of the output image.

**Key Point 5: Image Acquisition Technique — Using a Sensor Array (Digital Camera)**

> The most common technique involves a **2D sensor array** coupled with an **illumination source** and **optics**:
>
> 1. **Illumination:** The scene is illuminated by a light source (natural or artificial).
> 2. **Optics/Lens:** A lens focuses the reflected light onto the sensor array.
> 3. **Sensing:** Each sensor element converts the photon energy into an electrical voltage proportional to light intensity.
> 4. **Sampling:** The continuous image is sampled at discrete spatial locations (determined by the sensor grid).
> 5. **Quantization:** The continuous voltage at each sensor is converted to a discrete integer value (e.g., 0–255 for 8-bit).
> 6. **Output:** The result is a digital image f(x, y) stored as a 2D matrix of pixel values.

---

#### 📊 Diagram / Table (if applicable)

```
  (a) Single Sensor:               (b) Sensor Strip:
  ┌─────┐                          ┌─┬─┬─┬─┬─┬─┬─┬─┐
  │  S  │ ← moves in X & Y        │S│S│S│S│S│S│S│S│ ← moves in Y only
  └─────┘                          └─┴─┴─┴─┴─┴─┴─┴─┘
  ↕ ↔ (mechanical motion)              ↕ (motion in one direction)

  (c) Sensor Array:
  ┌─┬─┬─┬─┬─┬─┬─┬─┐
  │S│S│S│S│S│S│S│S│
  ├─┼─┼─┼─┼─┼─┼─┼─┤
  │S│S│S│S│S│S│S│S│  ← No motion required
  ├─┼─┼─┼─┼─┼─┼─┼─┤     (captures full 2D image at once)
  │S│S│S│S│S│S│S│S│
  ├─┼─┼─┼─┼─┼─┼─┼─┤
  │S│S│S│S│S│S│S│S│
  └─┴─┴─┴─┴─┴─┴─┴─┘

  Image Acquisition Pipeline:
  Scene → [Illumination] → [Lens/Optics] → [Sensor Array] → [Digitizer] → Digital Image
                                              (Sampling)      (Quantization)
```

---

#### 💡 Example

> A **digital camera** is a practical example of sensor array-based acquisition. The CMOS sensor array (e.g., 12 megapixels = 4000 × 3000) captures the entire scene in one shot. Light passes through the lens, hits the Bayer filter (colour filter array with R, G, B patterns), and each sensor converts photons to voltage. The ADC (Analog-to-Digital Converter) quantizes these voltages into 8-bit or higher values, producing the final digital image.

---

#### 🔚 Conclusion

> Image sensing and acquisition is the first and most critical step in digital image processing. Single sensors offer precision but are slow; sensor strips provide line-by-line capture at moderate speeds; and sensor arrays capture the entire image instantly, making them the standard in modern cameras. The choice of sensor arrangement depends on the application's requirements for speed, resolution, and cost. Modern image acquisition relies primarily on CCD and CMOS sensor arrays with integrated digitization.

---

---

## ❓ Question 4: Explain Bilinear Interpolation Method.

### ✅ Answer:

#### 📖 Definition / Introduction

**Bilinear interpolation** is a technique used in digital image processing to estimate the intensity value at a non-integer (sub-pixel) coordinate by using the weighted average of the four nearest pixel values. It is commonly used in image resizing (scaling), rotation, geometric transformation, and image registration. It produces smoother results than nearest-neighbour interpolation and is computationally less expensive than bicubic interpolation.

---

#### 📝 Detailed Explanation

**Key Point 1: Why Interpolation is Needed**

> When an image undergoes geometric transformations (scaling, rotation, translation), the transformed pixel coordinates often fall at **non-integer positions** in the original image. Since pixel values exist only at integer coordinates, we need to estimate (interpolate) the value at the fractional location. Bilinear interpolation uses the four closest known pixels to compute this estimate.

**Key Point 2: Mathematical Formulation**

> Given a point (x, y) where x and y are non-integer, the four nearest neighbours are:
>
> - f(x₁, y₁), f(x₁, y₂), f(x₂, y₁), f(x₂, y₂)
>
> where x₁ = floor(x), x₂ = x₁ + 1, y₁ = floor(y), y₂ = y₁ + 1.
>
> Let a = x − x₁ and b = y − y₁ (fractional parts, 0 ≤ a, b < 1).
>
> **Step 1 — Interpolate in X-direction (two linear interpolations):**
> - R₁ = (1−a) × f(x₁, y₁) + a × f(x₂, y₁)
> - R₂ = (1−a) × f(x₁, y₂) + a × f(x₂, y₂)
>
> **Step 2 — Interpolate in Y-direction (one linear interpolation):**
> - f(x, y) = (1−b) × R₁ + b × R₂
>
> **Combined Formula:**
> - f(x, y) = (1−a)(1−b) f(x₁,y₁) + a(1−b) f(x₂,y₁) + (1−a)b f(x₁,y₂) + ab f(x₂,y₂)

**Key Point 3: Properties of Bilinear Interpolation**

> - It performs **linear interpolation in two directions** (hence "bilinear").
> - It is **smoother** than nearest-neighbour interpolation (avoids blocky artefacts).
> - It may cause slight **blurring** of edges compared to bicubic interpolation.
> - It uses exactly **4 neighbouring pixels** for each computation.
> - Computational complexity is **moderate** — more than nearest-neighbour, less than bicubic.

---

#### 📊 Diagram / Table (if applicable)

```
  Four nearest pixels around point P(x, y):

     y₁          y₂
  x₁ ●───────────● 
     │  f(x₁,y₁) │ f(x₁,y₂)
     │            │
     │     P(x,y) │    b = y - y₁
     │      ×     │    a = x - x₁
     │            │
  x₂ ●───────────●
     f(x₂,y₁)     f(x₂,y₂)

  Step 1: Linear interpolation along x (rows):
    R₁ = lerp(f(x₁,y₁), f(x₂,y₁), a)   ← at y = y₁
    R₂ = lerp(f(x₁,y₂), f(x₂,y₂), a)   ← at y = y₂

  Step 2: Linear interpolation along y (columns):
    P  = lerp(R₁, R₂, b)

  Comparison Table:
  ┌─────────────────────┬──────────┬──────────┬──────────┐
  │ Method              │ Pixels   │ Quality  │ Speed    │
  │                     │ Used     │          │          │
  ├─────────────────────┼──────────┼──────────┼──────────┤
  │ Nearest-Neighbour   │ 1        │ Low      │ Fastest  │
  │ Bilinear            │ 4        │ Medium   │ Moderate │
  │ Bicubic             │ 16       │ High     │ Slowest  │
  └─────────────────────┴──────────┴──────────┴──────────┘
```

---

#### 💡 Example

> Suppose we want to find the intensity at point P(2.3, 4.7). The four nearest pixels are:
> - f(2, 4) = 100, f(3, 4) = 120, f(2, 5) = 140, f(3, 5) = 160
> - a = 0.3, b = 0.7
> - R₁ = (0.7)(100) + (0.3)(120) = 70 + 36 = 106
> - R₂ = (0.7)(140) + (0.3)(160) = 98 + 48 = 146
> - f(2.3, 4.7) = (0.3)(106) + (0.7)(146) = 31.8 + 102.2 = **134**

---

#### 🔚 Conclusion

> Bilinear interpolation is a widely used technique in image processing for estimating pixel values at non-integer coordinates. By performing two successive linear interpolations (first along one axis, then along the other), it produces smooth and visually pleasing results. It strikes a good balance between the blockiness of nearest-neighbour and the computational cost of bicubic interpolation, making it the default choice for many real-time image transformation applications.

---

---

## ❓ Question 5: What is the resolution of an image? Compute the size of a 640 × 480 image at 240 pixels per inch. What do you mean by digitization? Explain its two important steps.

### ✅ Answer:

#### 📖 Definition / Introduction

**Resolution** of a digital image refers to the level of spatial detail that the image can represent. It is typically described in terms of the number of pixels (spatial resolution) and the number of intensity levels (grey-level/intensity resolution). Resolution determines how much detail an image can convey and is a critical factor in image quality. **Digitization** is the process of converting a continuous (analog) image into a digital form.

---

#### 📝 Detailed Explanation

**Key Point 1: Image Resolution**

> Resolution can be described in multiple ways:
> - **Spatial Resolution:** The number of pixels per unit length (e.g., pixels per inch — PPI or dots per inch — DPI). Higher spatial resolution means more detail.
> - **Pixel Resolution:** Total pixel count, expressed as Width × Height (e.g., 640 × 480 = 307,200 pixels).
> - **Intensity/Grey-level Resolution:** The number of distinct intensity levels (e.g., 8-bit = 256 levels, 16-bit = 65,536 levels).
>
> A higher resolution image captures finer details but requires more storage.

**Key Point 2: Size Computation — 640 × 480 image at 240 PPI**

> Given:
> - Image dimensions: 640 × 480 pixels
> - Resolution: 240 pixels per inch (PPI)
>
> **Physical Size:**
> - Width = 640 / 240 = **2.67 inches**
> - Height = 480 / 240 = **2.0 inches**
>
> **Physical size of the image = 2.67 inches × 2.0 inches**
>
> **Storage Size (assuming 8-bit greyscale):**
> - Total pixels = 640 × 480 = 307,200 pixels
> - Storage = 307,200 × 8 bits = 2,457,600 bits = **300 KB** (approximately)
>
> For a 24-bit colour image: 307,200 × 24 = 7,372,800 bits = **900 KB** (approximately)

**Key Point 3: Digitization and Its Two Important Steps**

> **Digitization** is the process of converting a continuous analog image into a discrete digital image. It involves two fundamental steps:
>
> **Step 1: Sampling (Spatial Digitization)**
> - Sampling is the discretization of the **spatial coordinates** (x, y).
> - The continuous image is divided into a finite grid of M × N sample points (pixels).
> - Each sample corresponds to a specific location in the image.
> - The **sampling rate** determines the spatial resolution — higher sampling rate gives more pixels and finer detail.
> - According to the **Nyquist theorem**, the sampling rate must be at least **twice** the highest spatial frequency in the image to avoid aliasing.
>
> **Step 2: Quantization (Intensity Digitization)**
> - Quantization is the discretization of the **intensity values** (amplitude).
> - The continuous range of intensity values at each pixel is mapped to a finite set of L discrete levels (e.g., 256 levels for 8-bit quantization).
> - The number of quantization levels L = 2^k, where k is the number of bits per pixel.
> - Finer quantization (more levels) reduces quantization error and produces smoother intensity gradations.
> - Coarser quantization can produce visible **false contouring** artefacts.

---

#### 📊 Diagram / Table (if applicable)

```
  Digitization Process:

  Continuous Image f(x,y) ──→ [SAMPLING] ──→ [QUANTIZATION] ──→ Digital Image

  Sampling (Spatial):                Quantization (Intensity):
  ┌──────────────────┐               Continuous     Quantized
  │   Continuous     │               intensity      (L levels)
  │   image          │               ▲               ▲
  │   ╱╲╱╲╱╲╱╲╱╲   │               │ ╱╲            │ ┌─┐
  │                  │               │╱  ╲           │ │ │┌─┐
  │   ↓ Sample at    │               ╱    ╲          │ │ ││ │
  │   M × N points   │              ╱      ╲─        │─┘ │└─│
  │                  │                                └────────→
  │   ● ● ● ● ● ●   │
  │   ● ● ● ● ● ●   │              k = 8 bits → L = 256 levels
  │   ● ● ● ● ● ●   │              k = 1 bit  → L = 2 levels (binary)
  └──────────────────┘

  Size Calculation:
  ┌───────────────────────────────────────┐
  │ Width  = 640 pixels ÷ 240 PPI = 2.67"│
  │ Height = 480 pixels ÷ 240 PPI = 2.00"│
  │ Storage = 640 × 480 × 8 bits ≈ 300 KB│
  └───────────────────────────────────────┘
```

---

#### 💡 Example

> A photograph taken by a digital camera with a 12-megapixel sensor produces an image of 4000 × 3000 pixels (sampling) with each pixel stored as a 24-bit colour value (8 bits × 3 channels — quantization). The resulting uncompressed image size is 4000 × 3000 × 3 bytes ≈ 36 MB. When printed at 300 DPI, it produces a 13.3" × 10" print.

---

#### 🔚 Conclusion

> Image resolution defines the detail and quality of a digital image and is characterized by spatial and intensity resolution. Digitization converts continuous images to digital form through two essential steps: **sampling** (discretizing spatial coordinates) and **quantization** (discretizing intensity values). The balance between sampling rate, quantization levels, and storage requirements is a fundamental trade-off in digital imaging systems.

---

---

## ❓ Question 6: Write down the key stages in Digital Image Processing (DIP) and explain them. Explain different types of DIP processes.

### ✅ Answer:

#### 📖 Definition / Introduction

**Digital Image Processing (DIP)** refers to the use of computer algorithms to perform operations on digital images. The goal is to improve image quality, extract useful information, or transform images for specific applications. DIP involves a systematic pipeline of stages, each performing a specific function. Additionally, DIP processes can be categorized based on the level of abstraction — from low-level pixel operations to high-level semantic understanding.

---

#### 📝 Detailed Explanation

**Key Point 1: Key Stages in Digital Image Processing**

> **Stage 1 — Image Acquisition:**
> The first stage involves capturing the image using sensors (camera, scanner, satellite) and converting it to digital form. This includes sensing and digitization (sampling + quantization).
>
> **Stage 2 — Image Enhancement:**
> Improves the visual appearance of an image or converts it to a form better suited for analysis. Techniques include contrast stretching, histogram equalization, sharpening, and noise filtering.
>
> **Stage 3 — Image Restoration:**
> Aims to recover an image that has been degraded by a known or estimated degradation function. Unlike enhancement (subjective), restoration is **objective** and model-based. Examples: Wiener filter, inverse filtering.
>
> **Stage 4 — Colour Image Processing:**
> Deals with processing of colour images using colour models (RGB, HSI, CMYK). Includes colour transformations, colour-based segmentation, and pseudo-colouring.
>
> **Stage 5 — Wavelets and Multi-Resolution Processing:**
> Uses multi-resolution techniques like wavelet transforms to represent images at different scales. Foundation for image compression (JPEG 2000) and feature extraction.
>
> **Stage 6 — Compression:**
> Reduces the amount of data required to represent an image. Includes **lossless** (Huffman, LZW, Run-Length Encoding) and **lossy** (JPEG, JPEG 2000) techniques.
>
> **Stage 7 — Morphological Processing:**
> Uses shape-based operations (erosion, dilation, opening, closing) on binary/greyscale images for boundary extraction, hole filling, and connected component analysis.
>
> **Stage 8 — Image Segmentation:**
> Partitions an image into meaningful regions or objects. Techniques include thresholding, edge detection, region growing, and watershed algorithm. This is one of the most challenging stages.
>
> **Stage 9 — Representation and Description:**
> After segmentation, regions are represented (boundary, skeleton) and described using features (shape descriptors, texture, colour histograms) for recognition.
>
> **Stage 10 — Object Recognition:**
> Assigns a label or meaning to an object based on its description. Uses pattern matching, machine learning, and deep learning. This is the highest level of DIP.

**Key Point 2: Types of DIP Processes**

> **(a) Low-Level Processing:**
> - Input: Image → Output: Image
> - Involves primitive operations like noise reduction, contrast enhancement, sharpening.
> - Examples: Filtering, histogram equalization, edge detection.
>
> **(b) Mid-Level Processing:**
> - Input: Image → Output: Attributes/Features
> - Involves segmentation, classification, and feature extraction.
> - Examples: Object detection, region labelling, feature descriptors.
>
> **(c) High-Level Processing:**
> - Input: Attributes → Output: Understanding/Interpretation
> - Involves making sense of recognized objects, scene understanding.
> - Examples: Autonomous navigation, medical diagnosis, facial recognition.

---

#### 📊 Diagram / Table (if applicable)

```
  Key Stages in DIP (Pipeline):

  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
  │   Image      │───→│   Image      │───→│   Image      │
  │ Acquisition  │    │ Enhancement  │    │ Restoration  │
  └──────────────┘    └──────────────┘    └──────────────┘
         │                                       │
         ↓                                       ↓
  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
  │   Colour     │───→│  Wavelets &  │───→│  Compression │
  │  Processing  │    │ Multi-Res.   │    │              │
  └──────────────┘    └──────────────┘    └──────────────┘
                                                 │
         ┌───────────────────────────────────────┘
         ↓
  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
  │ Morphological│───→│   Image      │───→│Representation│
  │  Processing  │    │ Segmentation │    │& Description │
  └──────────────┘    └──────────────┘    └──────────────┘
                                                 │
                                                 ↓
                                          ┌──────────────┐
                                          │   Object     │
                                          │ Recognition  │
                                          └──────────────┘

  Types of DIP Processes:
  ┌─────────────────┬───────────────┬────────────────────────┐
  │ Level           │ Input→Output  │ Example                │
  ├─────────────────┼───────────────┼────────────────────────┤
  │ Low-Level       │ Image→Image   │ Filtering, Enhancement │
  │ Mid-Level       │ Image→Attrib. │ Segmentation, Features │
  │ High-Level      │ Attrib.→Under.│ Recognition, Analysis  │
  └─────────────────┴───────────────┴────────────────────────┘
```

---

#### 💡 Example

> In a **medical X-ray analysis system**: Image acquisition captures the X-ray (Stage 1). Enhancement improves contrast (Stage 2). Restoration removes blur from patient motion (Stage 3). Segmentation identifies regions of interest like tumours (Stage 8). Feature extraction measures tumour size and shape (Stage 9). Finally, recognition classifies the tumour as benign or malignant (Stage 10).

---

#### 🔚 Conclusion

> Digital Image Processing follows a well-defined pipeline of stages, from acquisition to recognition. Each stage builds on the output of the previous one, progressively moving from raw pixel data to high-level understanding. DIP processes can be classified into low-level (image-to-image), mid-level (image-to-features), and high-level (features-to-understanding) processing, each serving a distinct purpose in the image analysis pipeline.

---

---

## ❓ Question 7: What is an 8-bit colour image? Explain. What is meant by classification of image?

### ✅ Answer:

#### 📖 Definition / Introduction

An **8-bit colour image** is a digital image where each pixel's colour is represented using 8 bits (1 byte) of data, allowing for a maximum of **2⁸ = 256 distinct colours**. This is in contrast to full-colour images (24-bit or higher) that can represent millions of colours. **Classification of images** refers to the categorization of digital images based on their data representation, colour depth, and dimensionality.

---

#### 📝 Detailed Explanation

**Key Point 1: 8-Bit Colour Image**

> In an 8-bit colour image, each pixel stores a single 8-bit value (0–255) that serves as an **index** into a **colour lookup table (CLUT)** or **palette**. The palette contains up to 256 entries, where each entry specifies the actual colour (usually as 24-bit RGB values — 8 bits each for Red, Green, Blue).
>
> - The pixel value does NOT directly represent colour; it is a **pointer** to the palette.
> - The palette is chosen to best represent the colours in the image (using algorithms like median-cut or octree quantization).
> - This format is also known as an **indexed colour image** or **palette-based image**.
>
> **Note:** An 8-bit **greyscale** image also uses 8 bits per pixel, but each value directly represents intensity (0 = black, 255 = white) with no palette.

**Key Point 2: Advantages and Limitations**

> **Advantages:**
> - Requires significantly less memory (8 bits vs. 24 bits per pixel — 3× less).
> - Faster processing and transmission.
> - Suitable for images with limited colour range (logos, icons, simple graphics).
>
> **Limitations:**
> - Only 256 colours can be displayed simultaneously.
> - Not suitable for photographs or complex natural scenes.
> - Colour banding artefacts may appear in smooth gradients.

**Key Point 3: Classification of Images**

> Digital images can be classified based on various criteria:
>
> **(a) Based on Colour Depth / Type:**
> - **Binary Image (1-bit):** Each pixel is either 0 (black) or 1 (white). Used for documents, text recognition.
> - **Greyscale Image (8-bit):** Each pixel has 256 intensity levels (0–255). Used for medical imaging, document analysis.
> - **Colour Image (24-bit / True Colour):** Each pixel has 3 channels (R, G, B), 8 bits each = 16.7 million colours. Used for photography, display.
> - **8-bit Colour (Indexed):** 256 colours from a palette (as described above).
> - **High Dynamic Range (HDR):** Uses 16-bit or 32-bit per channel for extended dynamic range.
>
> **(b) Based on Dimensionality:**
> - **2D Images:** Standard photographs, X-rays (single 2D plane).
> - **3D Images:** Volumetric data like CT/MRI scans (stack of 2D slices).
> - **Video/Sequence:** Temporal sequence of 2D images.
>
> **(c) Based on Source/Application:**
> - Visible light images, infrared images, X-ray images, ultrasound images, satellite images, etc.

---

#### 📊 Diagram / Table (if applicable)

```
  8-bit Colour Image Structure:

  Image (M × N pixels)           Colour Palette (CLUT)
  ┌────┬────┬────┬────┐         ┌───────┬─────────────────┐
  │ 05 │ 12 │ 200│ 45 │         │ Index │  R    G    B    │
  ├────┼────┼────┼────┤         ├───────┼─────────────────┤
  │ 78 │ 03 │ 156│ 99 │   →     │  00   │ 0    0    0    │
  ├────┼────┼────┼────┤  lookup  │  01   │ 128  0    0    │
  │ 45 │ 200│ 12 │ 03 │         │  ...  │ ...  ...  ...  │
  ├────┼────┼────┼────┤         │  05   │ 255  128  64   │
  │ 12 │ 99 │ 78 │ 05 │         │  ...  │ ...  ...  ...  │
  └────┴────┴────┴────┘         │  255  │ 255  255  255  │
  (Each value = palette index)  └───────┴─────────────────┘

  Image Classification:
  ┌──────────────────┬────────────┬───────────────────┐
  │ Type             │ Bits/Pixel │ Distinct Values   │
  ├──────────────────┼────────────┼───────────────────┤
  │ Binary           │ 1          │ 2                 │
  │ Greyscale        │ 8          │ 256               │
  │ 8-bit Colour     │ 8 (indexed)│ 256 (from palette)│
  │ True Colour      │ 24         │ 16,777,216        │
  │ HDR              │ 32–96      │ Billions+         │
  └──────────────────┴────────────┴───────────────────┘
```

---

#### 💡 Example

> The **GIF image format** uses 8-bit indexed colour. When a 24-bit photograph is converted to GIF, the software selects the 256 most representative colours and creates a palette. Each pixel is then mapped to the closest palette colour. This explains why GIF images often look "banded" or less smooth compared to JPEG images that use full 24-bit colour.

---

#### 🔚 Conclusion

> An 8-bit colour image uses indexed colour representation where each pixel's 8-bit value indexes into a palette of 256 colours. While memory-efficient, it is limited in colour range compared to true-colour images. Image classification helps us categorize images based on colour depth (binary, greyscale, indexed, true colour), dimensionality (2D, 3D), and application domain, enabling appropriate processing techniques to be applied.

---

---

## ❓ Question 8: What is aliasing in the context of image sampling? What do you mean by image file format? Mention some commonly used image file formats.

### ✅ Answer:

#### 📖 Definition / Introduction

**Aliasing** is a distortion or artefact that occurs when a continuous image is sampled at a rate insufficient to capture its detail (i.e., below the Nyquist rate). It manifests as false patterns, jagged edges ("jaggies"), or moiré effects in the digital image. An **image file format** defines the structure and encoding method used to store a digital image on disk, including how pixel data, metadata, and compression are organized.

---

#### 📝 Detailed Explanation

**Key Point 1: Aliasing in Image Sampling**

> When a continuous image is digitized through sampling, the sampling rate must be high enough to capture all spatial frequencies present in the image. According to the **Nyquist-Shannon Sampling Theorem**, the sampling frequency must be **at least twice** the highest frequency component in the image.
>
> **If sampling rate < 2 × f_max (highest frequency):**
> - High-frequency components (fine details, sharp edges) are incorrectly represented as lower frequencies.
> - This phenomenon is called **aliasing** — the high frequencies "masquerade" as low frequencies.
>
> **Common aliasing artefacts include:**
> - **Jagged edges (Jaggies):** Staircase-like appearance of diagonal/curved lines.
> - **Moiré patterns:** False repetitive patterns appear when sampling fine regular patterns (e.g., a brick wall, fabric weave).
> - **Loss of fine detail:** Small features disappear or merge.

**Key Point 2: Anti-Aliasing Techniques**

> - **Increase sampling rate:** Use more pixels (higher resolution sensor).
> - **Pre-filtering (Low-pass filtering):** Blur the image slightly before sampling to remove frequencies above the Nyquist limit. This is done optically using an anti-aliasing filter placed before the sensor.
> - **Super-sampling:** Sample at a higher rate, then downsample with filtering.

**Key Point 3: Image File Format**

> An **image file format** specifies:
> - How pixel data is organized and stored (row-major, planar, etc.).
> - The compression method used (if any).
> - Metadata (resolution, colour space, creation date, etc.).
> - Colour depth and colour model (RGB, CMYK, indexed).
>
> **Commonly Used Image File Formats:**
>
> | Format | Full Name | Compression | Key Features |
> |--------|-----------|-------------|--------------|
> | **JPEG** | Joint Photographic Experts Group | Lossy (DCT-based) | Best for photographs, adjustable quality |
> | **PNG** | Portable Network Graphics | Lossless (Deflate) | Supports transparency (alpha), web graphics |
> | **GIF** | Graphics Interchange Format | Lossless (LZW) | 256 colours, supports animation |
> | **BMP** | Bitmap | Usually uncompressed | Simple format, large file size |
> | **TIFF** | Tagged Image File Format | Lossless/Lossy | Professional photography, publishing |
> | **RAW** | Camera Raw | None/Lossless | Unprocessed sensor data, maximum quality |
> | **SVG** | Scalable Vector Graphics | N/A (vector) | Resolution-independent, web graphics |
> | **WEBP** | Web Picture | Lossy/Lossless | Modern web format by Google, smaller than JPEG/PNG |

---

#### 📊 Diagram / Table (if applicable)

```
  Aliasing due to Under-sampling:

  Original Signal (High Frequency):
  ╱╲╱╲╱╲╱╲╱╲╱╲╱╲╱╲╱╲╱╲╱╲    (Fine detail)

  Sampled at Sufficient Rate (≥ 2× f_max):
  ●  ●  ●  ●  ●  ●  ●  ●     → Correct reconstruction

  Under-sampled (< 2× f_max):
  ●        ●        ●         → Alias! Appears as low frequency
  ╲      ╱    ╲      ╱
    ╲  ╱        ╲  ╱           (False low-frequency pattern)


  Moiré Pattern Example:
  Original: |||||||||||||||    (fine vertical lines)
  Sampled:  |  |  |  |  |     (coarser pattern appears — moiré)


  Nyquist Theorem:
  f_sampling ≥ 2 × f_max  →  No aliasing
  f_sampling < 2 × f_max  →  Aliasing occurs
```

---

#### 💡 Example

> When photographing a person wearing a **finely striped shirt** with a digital camera, the stripes may appear as wavy, shifting colour patterns (moiré) in the captured image. This is aliasing — the spatial frequency of the stripe pattern exceeds the Nyquist limit of the camera sensor. Many cameras include an **optical low-pass (anti-aliasing) filter** in front of the sensor to mitigate this effect.

---

#### 🔚 Conclusion

> Aliasing is a fundamental sampling artefact that occurs when the sampling rate is insufficient to represent the image's spatial frequencies accurately. It can be mitigated through higher sampling rates or pre-filtering techniques. Image file formats define how digital images are stored and vary in compression methods, colour support, and intended applications. Choosing the right format depends on the trade-off between quality, file size, and application requirements.

---

---

## ❓ Question 9: Differentiate between an image and a scene. Define a digital image and explain image pixels. What is digitization of an image?

### ✅ Answer:

#### 📖 Definition / Introduction

In image processing, the terms **image** and **scene** are related but distinct concepts. A **scene** is the actual physical 3D environment, while an **image** is a 2D representation of that scene captured by a sensor. A **digital image** is a numerical (discrete) representation of a 2D image, and its fundamental building blocks are **pixels**. **Digitization** is the process of converting a continuous image into this discrete digital form.

---

#### 📝 Detailed Explanation

**Key Point 1: Difference Between Image and Scene**

> | Aspect | Scene | Image |
> |--------|-------|-------|
> | **Definition** | The actual 3D physical world or environment being observed | A 2D representation of the scene captured by an imaging device |
> | **Dimensionality** | Three-dimensional (3D) | Two-dimensional (2D) |
> | **Nature** | Physical, real-world, continuous | Projected, captured, can be continuous or digital |
> | **Information** | Contains complete depth, texture, and spatial information | Contains partial information (projection of 3D onto 2D) |
> | **Existence** | Exists independently of any observer or device | Created by an imaging system (camera, scanner, etc.) |
> | **Example** | A landscape with mountains, rivers, and trees | A photograph of that landscape |

**Key Point 2: Digital Image**

> A **digital image** is a 2D function f(x, y) where:
> - **x** and **y** are discrete spatial coordinates (integer values).
> - **f(x, y)** is the intensity or colour value at coordinates (x, y), also a discrete quantity.
>
> Mathematically, a digital image is a **matrix** (or 2D array) of size M × N, where M is the number of rows and N is the number of columns. Each element of this matrix is a pixel.
>
> A digital image can be represented as:
> f(x, y) where x = 0, 1, 2, ..., M−1 and y = 0, 1, 2, ..., N−1
> and f ∈ {0, 1, 2, ..., L−1} where L is the number of grey levels.

**Key Point 3: Image Pixels**

> A **pixel** (picture element) is the smallest individual element of a digital image. Key properties:
> - Each pixel has a specific **spatial location** (x, y) in the image grid.
> - Each pixel holds a **value** representing intensity (greyscale) or colour (RGB/multi-channel).
> - Pixels are arranged in a **rectangular grid** of rows and columns.
> - The total number of pixels = M × N (spatial resolution).
> - Pixel values are **discrete integers** resulting from quantization.

**Key Point 4: Digitization of an Image**

> Digitization converts a **continuous analog image** into a **discrete digital image** through two steps:
>
> **Sampling:** Discretization of spatial coordinates. The continuous (x, y) plane is divided into a finite grid of M × N discrete points. Each point becomes a pixel location. The sampling rate determines the spatial resolution.
>
> **Quantization:** Discretization of intensity values. The continuous range of brightness/colour at each sampled point is mapped to one of L discrete levels. For k-bit quantization, L = 2^k levels.
>
> After digitization: f(x, y) → a matrix of M × N pixels, each with an integer value from 0 to L−1.

---

#### 📊 Diagram / Table (if applicable)

```
  Scene vs. Image:

  3D Scene (Real World)          2D Image (Captured)
  ┌─────────────────┐            ┌─────────────────┐
  │   /\  Mountain  │            │   /\             │
  │  /  \    Sun ☀  │   Camera   │  /  \    ☀      │
  │ /    \  ~~~     │  ───────→  │ /    \  ~~~     │
  │/______\ River   │  (Sensing  │/______\         │
  │ Trees  🌳🌳    │  + Digitiz.)│ 🌳🌳           │
  └─────────────────┘            └─────────────────┘
  (3D, continuous, real)         (2D, discrete, digital)

  Digital Image as a Matrix:
  f(x,y) = ┌─────┬─────┬─────┬─────┐
           │f(0,0)│f(0,1)│f(0,2)│...  │  ← Row 0
           ├─────┼─────┼─────┼─────┤
           │f(1,0)│f(1,1)│f(1,2)│...  │  ← Row 1
           ├─────┼─────┼─────┼─────┤
           │ ... │ ... │ ... │...  │
           ├─────┼─────┼─────┼─────┤
           │f(M-1,0)│...│...  │...  │  ← Row M-1
           └─────┴─────┴─────┴─────┘
            Col 0  Col 1  Col 2

  Each f(x,y) is a PIXEL with value ∈ {0, 1, ..., L-1}
```

---

#### 💡 Example

> When you stand in front of a garden (scene), your eyes perceive a continuous 3D world with infinite colour variations. When you take a photograph with a 12MP digital camera, the sensor samples this scene into 4000 × 3000 discrete pixels (sampling) and converts each point's light intensity into one of 256 levels per colour channel (quantization), producing a digital image — a 2D discrete representation of the original 3D scene.

---

#### 🔚 Conclusion

> A scene is the physical 3D world, while an image is its 2D projection captured by an imaging device. A digital image is a discrete matrix of pixels, where each pixel represents a sampled and quantized intensity value at a specific spatial location. Digitization — the process of converting continuous images to digital form through sampling and quantization — is the foundational step that makes computer-based image processing possible.

---

---

## ❓ Question 10: Brightness discrimination is poor at low levels of illumination. Explain. What is Weber ratio? Show the variation of Weber ratio for humans. What is colour image processing? What is brightness adaptation?

### ✅ Answer:

#### 📖 Definition / Introduction

The human visual system's ability to discriminate between different brightness levels is not uniform — it is significantly **poorer at low illumination levels** compared to well-lit conditions. This behaviour is described by the **Weber ratio**, a fundamental concept in visual perception. Understanding these properties of human vision is essential for designing effective image processing systems. **Colour image processing** and **brightness adaptation** are closely related concepts in the study of visual perception and digital image processing.

---

#### 📝 Detailed Explanation

**Key Point 1: Poor Brightness Discrimination at Low Illumination**

> The human eye can perceive a vast range of illumination levels (from dim starlight to bright sunlight — about 10^10 range). However, at any given adaptation level, the eye can only discriminate a limited range of brightness (called the **simultaneous dynamic range**, roughly 1:100 or ~1000 levels).
>
> At **low illumination levels** (scotopic vision — rod-dominated):
> - The eye uses **rod cells**, which are more sensitive to light but cannot distinguish colours and have low spatial resolution.
> - The ability to detect small differences in brightness (ΔI) between adjacent regions is **poor**.
> - A larger absolute change in intensity is needed to perceive a difference.
>
> At **high illumination levels** (photopic vision — cone-dominated):
> - The eye uses **cone cells**, which provide colour vision and higher resolution.
> - Brightness discrimination is **better** — smaller differences can be detected.

**Key Point 2: Weber Ratio**

> The **Weber ratio** quantifies the minimum detectable change in intensity relative to the background intensity:
>
> **Weber Ratio = ΔI_c / I**
>
> Where:
> - **I** = background intensity (current illumination level)
> - **ΔI_c** = increment of illumination (Just Noticeable Difference — JND), the smallest change in intensity that is perceptible by the eye at intensity level I.
>
> **A small Weber ratio** means the eye can discriminate fine differences in brightness (good discrimination).
> **A large Weber ratio** means coarse discrimination (poor sensitivity to differences).
>
> **Weber's Law** states that ΔI_c / I ≈ constant over a wide range of illumination levels (approximately 0.02 for well-adapted human vision in moderate-to-bright light). However, this breaks down at very low illumination levels.

**Key Point 3: Variation of Weber Ratio for Humans**

> The Weber ratio is **NOT constant** across all illumination levels:
>
> - At **very low intensity** (scotopic/dim): Weber ratio is **high** (~0.1 or more) — poor discrimination.
> - As intensity increases, the ratio **decreases** rapidly.
> - At **moderate to high intensity** (photopic): Weber ratio plateaus at approximately **0.02** — good discrimination.
> - At **very high intensity** (glare): The ratio may increase again slightly.
>
> This means humans are best at discriminating brightness differences in well-lit conditions, not in darkness or extreme brightness.

**Key Point 4: Brightness Adaptation**

> **Brightness adaptation** (or **luminance adaptation**) is the ability of the human visual system to adjust its sensitivity based on the overall illumination level. The eye adapts to the average brightness of the scene by adjusting:
> - **Pupil size** (mechanical adjustment — faster but limited range).
> - **Photochemical changes** in rod and cone cells (slower but covers a wider range).
>
> The total range of adaptation spans about **10 orders of magnitude** (10^−6 to 10^4 candelas/m²), but at any single adaptation level, the eye can only discriminate about **100–200 distinct intensity levels** simultaneously.

**Key Point 5: Colour Image Processing**

> **Colour image processing** is the area of DIP that deals with processing images where colour information is present. It is divided into two major areas:
>
> **(a) Pseudo-colour (False colour) processing:** Assigning colours to greyscale images based on intensity to enhance visualization (e.g., thermal imaging, satellite imagery).
>
> **(b) Full-colour processing:** Processing images that are naturally acquired in colour (e.g., RGB photographs). Operations include colour transformations, colour-based segmentation, colour histogram analysis, and colour space conversions (RGB ↔ HSI ↔ CMYK).
>
> Colour adds three independent channels of information, enabling operations that are impossible with greyscale alone (e.g., separating objects by hue).

---

#### 📊 Diagram / Table (if applicable)

```
  Weber Ratio Variation for Humans:

  Weber Ratio
  (ΔIc/I)
    |
  0.10 ┤ ●                          (Poor discrimination
    |   \                            at low light)
  0.08 ┤  \
    |    \
  0.06 ┤   \
    |     \
  0.04 ┤     \
    |       \
  0.02 ┤--------●────────────────●   (Good discrimination
    |        (Weber's Law region)     in bright light)
  0.00 ┤
    └──┬──────┬──────┬──────┬──→  log(Intensity I)
      Low   Medium   High   Very High
    (Scotopic)      (Photopic)

  Brightness Adaptation Range:
  ←── Full adaptation range: ~10^10 ──→
  ←── Simultaneous range at one level: ~10^2 ──→

  Colour Image Processing:
  ┌─────────────────────────────────────────┐
  │  Pseudo-colour    │   Full-colour       │
  │  (Grey → Colour)  │   (Natural colour)  │
  │  Thermal maps     │   RGB photographs   │
  │  Medical scans    │   Colour segment.   │
  └─────────────────────────────────────────┘
```

---

#### 💡 Example

> When driving at night (low illumination), it is difficult to distinguish between dark grey and black objects on the road (high Weber ratio = poor discrimination). In daylight (high illumination), the same objects are easily distinguishable (low Weber ratio). When you walk from a dark movie theatre into bright sunlight, your eyes take several seconds to adapt (brightness adaptation) — during this transition, your discrimination ability is temporarily impaired.

---

#### 🔚 Conclusion

> The human eye's brightness discrimination ability varies with illumination level, being poorest in dim conditions and best in moderate-to-bright light. The Weber ratio (ΔIc/I) quantifies this behaviour and is approximately constant (~0.02) in the photopic range but increases significantly in scotopic conditions. Brightness adaptation allows the eye to operate across an enormous range of illumination levels, though only a limited range is discriminable at any one adaptation level. Colour image processing leverages colour information beyond greyscale to enable richer analysis and visualization.

---

---

## ❓ Question 11: What are the storage requirements for: (a) A 500 × 500 binary image? (b) A 1024 × 1024 binary image?

### ✅ Answer:

#### 📖 Definition / Introduction

The **storage requirement** of a digital image depends on its spatial dimensions (number of pixels) and its bit depth (number of bits used to represent each pixel). A **binary image** uses only **1 bit per pixel**, where each pixel is either 0 (black) or 1 (white). Calculating storage requirements is fundamental to understanding image processing system design, memory allocation, and transmission bandwidth.

---

#### 📝 Detailed Explanation

**Key Point 1: Storage Formula**

> The storage required for an uncompressed digital image is given by:
>
> **Storage = M × N × k bits**
>
> Where:
> - M = number of rows (height in pixels)
> - N = number of columns (width in pixels)
> - k = number of bits per pixel (bit depth)
>
> For a **binary image**, k = 1 bit per pixel.

**Key Point 2: (a) 500 × 500 Binary Image**

> - M = 500, N = 500, k = 1 bit
> - Storage = 500 × 500 × 1 = **250,000 bits**
> - In bytes: 250,000 / 8 = **31,250 bytes**
> - In kilobytes: 31,250 / 1024 ≈ **30.52 KB**

**Key Point 3: (b) 1024 × 1024 Binary Image**

> - M = 1024, N = 1024, k = 1 bit
> - Storage = 1024 × 1024 × 1 = **1,048,576 bits**
> - In bytes: 1,048,576 / 8 = **131,072 bytes**
> - In kilobytes: 131,072 / 1024 = **128 KB**
> - In megabits: 1,048,576 / 1,000,000 ≈ **1.05 Mbits**

---

#### 📊 Diagram / Table (if applicable)

```
  Storage Comparison Table:

  ┌──────────────────┬────────┬──────────────┬──────────────┬──────────┐
  │ Image Size       │ Bits/  │ Total Bits   │ Total Bytes  │ Approx.  │
  │                  │ Pixel  │              │              │ Size     │
  ├──────────────────┼────────┼──────────────┼──────────────┼──────────┤
  │ 500 × 500        │ 1      │ 250,000      │ 31,250       │ 30.52 KB │
  │ (binary)         │        │              │              │          │
  ├──────────────────┼────────┼──────────────┼──────────────┼──────────┤
  │ 1024 × 1024      │ 1      │ 1,048,576    │ 131,072      │ 128 KB   │
  │ (binary)         │        │              │              │          │
  ├──────────────────┼────────┼──────────────┼──────────────┼──────────┤
  │ For comparison:  │        │              │              │          │
  │ 1024 × 1024      │ 8      │ 8,388,608    │ 1,048,576    │ 1 MB     │
  │ (8-bit grey)     │        │              │              │          │
  ├──────────────────┼────────┼──────────────┼──────────────┼──────────┤
  │ 1024 × 1024      │ 24     │ 25,165,824   │ 3,145,728    │ 3 MB     │
  │ (24-bit colour)  │        │              │              │          │
  └──────────────────┴────────┴──────────────┴──────────────┴──────────┘

  Note: These are UNCOMPRESSED storage requirements.
  Actual file sizes may be smaller with compression (e.g., RLE for binary images).
```

---

#### 💡 Example

> A fax machine transmits binary images of documents. A standard A4 page scanned at 200 DPI produces an image of approximately 1700 × 2340 pixels. Storage = 1700 × 2340 × 1 = 3,978,000 bits ≈ 485 KB (uncompressed). Using Group 3 fax compression (a form of run-length encoding), this can typically be compressed to 30–50 KB, making transmission over phone lines feasible.

---

#### 🔚 Conclusion

> Storage requirements for digital images are directly determined by the image dimensions and bit depth. A 500 × 500 binary image requires approximately **30.52 KB**, while a 1024 × 1024 binary image requires **128 KB** of uncompressed storage. Binary images are the most storage-efficient format but can only represent two intensity levels. Understanding storage requirements is crucial for system design, particularly in applications involving large volumes of images or real-time transmission.

---

---

> 💡 *More questions will be added as provided by Rishav.*

---

*📑 Documented by Rishav | Wishing you all the very best in your upcoming examinations! 🌟🎓*
