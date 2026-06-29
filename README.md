UnHere are the answers to all 22 questions from your Image Processing exam sheet, structured concisely to fit a typical **5-mark** university standard.

---

## Unit 1

### 1. What is an 8-bit color image? For what purpose could it be used?

An **8-bit color image** is a digital image where each pixel is represented by an 8-bit integer, allowing for a maximum of $2^8 = 256$ possible colors. Instead of storing direct RGB values per pixel (which takes 24 bits), it typically uses an **indexed color model**. The 8-bit value serves as an index pointing to a Color Lookup Table (LUT) that contains the actual 24-bit RGB values.

**Purposes/Applications:**

* **Web Graphics:** Widely used in legacy web formats like GIF and indexed PNG to ensure fast loading times over slow networks.
* **Medical Imaging:** Used in simple ultrasound or X-ray displays where 256 shades of gray or pseudo-colors are sufficient.
* **Legacy Gaming & Graphics:** Essential for retro video games and older operating systems to optimize limited VRAM and processing power.

### 2. Write down the key stages in digital image processing and explain it.

Digital image processing involves several key sequential stages to alter or extract information from an image:

* **Image Acquisition:** Converting a physical scene into a digital format using sensors (e.g., a digital camera).
* **Image Enhancement:** Improving the visual quality of an image for human viewing (e.g., contrast stretching, noise filtering) without altering the information content.
* **Image Restoration:** Modeling and removing degradations (like blur or sensor noise) to reconstruct the original, uncorrupted image.
* **Color Image Processing:** Handling color spaces, color balance, and color enhancements.
* **Wavelets & Multiresolution Processing:** Representing images at various degrees of resolution for compression or analysis.
* **Compression:** Reducing the storage space or bandwidth required to transmit an image (e.g., JPEG).
* **Morphological Processing:** Extracting image components useful in representing and describing region shapes (e.g., erosion, dilation).
* **Segmentation:** Partitioning an image into its constituent parts or objects (e.g., background vs. foreground).
* **Representation & Description:** Turning raw segmented data into a form suitable for computer processing (e.g., boundary or regional features).
* **Object Recognition:** Assigning a label to an object based on its descriptors (e.g., identifying a car).

---

## Unit 2

### 3. Write down various geometric transformations.

Geometric transformations alter the spatial arrangement of pixels in an image. They map pixel positions from an input image coordinates $(x, y)$ to an output image coordinates $(x', y')$. The primary affine transformations include:

* **Translation:** Shifting an image horizontally by $t_x$ and vertically by $t_y$.

$$\begin{bmatrix} x' \\ y' \\ 1 \end{bmatrix} = \begin{bmatrix} 1 & 0 & t_x \\ 0 & 1 & t_y \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$$


* **Scaling:** Resizing an image horizontally by $s_x$ and vertically by $s_y$.

$$\begin{bmatrix} x' \\ y' \\ 1 \end{bmatrix} = \begin{bmatrix} s_x & 0 & 0 \\ 0 & s_y & 0 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$$


* **Rotation:** Rotating an image by an angle $\theta$ around the origin.

$$\begin{bmatrix} x' \\ y' \\ 1 \end{bmatrix} = \begin{bmatrix} \cos\theta & -\sin\theta & 0 \\ \sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$$


* **Shearing:** Distorting an image along an axis. Horizontal shear uses a factor $h_x$:

$$\begin{bmatrix} x' \\ y' \\ 1 \end{bmatrix} = \begin{bmatrix} 1 & h_x & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$$



### 4. What do you mean by sampling and quantization? Explain its function in digital image processing.

An image captured by a sensor is continuous in space and amplitude. To convert it to a digital format, it must undergo sampling and quantization:

* **Sampling:** Digitizing the **spatial coordinates** $(x, y)$. It determines the spatial resolution (or pixel grid density) of the image.
* **Quantization:** Digitizing the **amplitude** (intensity/gray level) values. It determines the number of discrete gray levels or colors available per pixel.

**Function in Digital Image Processing:**

* They act as the bridge between the analog world and the digital world.
* **Sampling** controls the fine detail or sharpness; undersampling leads to pixelation or aliasing.
* **Quantization** controls the smooth transition of tones; under-quantization causes "false contouring" effects.

---

## Unit 3

### 5. Discuss briefly about the discrete cosine transform (DCT).

The **Discrete Cosine Transform (DCT)** expresses a finite sequence of data points in terms of a sum of cosine functions oscillating at different frequencies. In image processing, the 2D-DCT transforms an image from the spatial domain to the frequency domain.

The forward 2D-DCT formula for an $N \times N$ image block is:


$$F(u, v) = \alpha(u)\alpha(v) \sum_{x=0}^{N-1} \sum_{y=0}^{N-1} f(x, y) \cos \left[ \frac{(2x+1)u\pi}{2N} \right] \cos \left[ \frac{(2y+1)v\pi}{2N} \right]$$

**Key Characteristics and Uses:**

* **Energy Compaction:** It packs the most visually significant information of the image into just a few low-frequency coefficients (top-left corner).
* **Image Compression:** It forms the backbone of the **JPEG** image compression standard, allowing high-frequency noise/details to be discarded during quantization without significant loss in perceptual quality.

### 6. What is pixel? Explain 4-neighbor, 8-neighbor of a pixel. Explain m-adjacency.

A **pixel** (picture element) is the smallest addressable unit or point in a digital image, possessing a specific coordinate and intensity value.

**Neighbors of a Pixel $P(x,y)$:**

* **4-neighbors ($N_4(P)$):** The four horizontal and vertical pixels adjacent to $P$.

$$\{(x+1, y), (x-1, y), (x, y+1), (x, y-1)\}$$


* **8-neighbors ($N_8(P)$):** The 4-neighbors plus the four diagonal neighbors.

$$N_8(P) = N_4(P) \cup \{(x+1, y+1), (x+1, y-1), (x-1, y+1), (x-1, y-1)\}$$



**m-adjacency (Mixed Adjacency):**
Two pixels $p$ and $q$ with intensity values from a set $V$ are $m$-adjacent if:

1. $q$ is in $N_4(p)$, OR
2. $q$ is in $N_D(p)$ (diagonal neighbors) AND the intersection $N_4(p) \cap N_4(q)$ has no pixels with values from $V$.
*Function:* It eliminates the ambiguity of multiple paths that can occur in 8-adjacency.

### 7. What is boundary descriptor? Explain Fourier descriptor.

A **boundary descriptor** is a quantitative metric used to characterize and represent the external shape (boundary) of a segmented region in an image, facilitating object recognition. Examples include length, curvature, and chain codes.

**Fourier Descriptors:**
Fourier descriptors represent a 2D boundary path using a 1D sequence of complex numbers. If a boundary has $K$ pixels, it can be tracked as a sequence of coordinate pairs $(x_k, y_k)$ rewritten as complex numbers:


$$s(k) = x_k + j y_k \quad \text{for } k = 0, 1, 2, \dots, K-1$$

Taking the Discrete Fourier Transform (DFT) yields the Fourier descriptors $a(u)$:


$$a(u) = \frac{1}{K} \sum_{k=0}^{K-1} s(k) e^{-j2\pi uk / K}$$

* **Advantage:** By discarding high-frequency coefficients, we get a smoothed boundary representation. They can be normalized to be invariant to rotation, translation, and scaling.

---

## Unit 4

### 8. Distinguish between image enhancement and image restoration.

| Feature | Image Enhancement | Image Restoration |
| --- | --- | --- |
| **Objective** | Improve image quality for **human interpretation** or subjective appeal. | Reconstruct or recover an image that has been degraded using an **objective mathematical model**. |
| **Approach** | Subjective, heuristic, and interactive (trial and error). | Objective and deterministic. |
| **Domain Knowledge** | Does not require knowledge of how the image was degraded. | Requires a mathematical model of the degradation function (e.g., blur, motion). |
| **Example Methods** | Contrast stretching, histogram equalization, sharpening filters. | Wiener filtering, Inverse filtering, Lucy-Richardson deconvolution. |

### 9. What is Gaussian noise? What is salt and pepper noise?

* **Gaussian Noise:** Also known as electronic noise, its probability density function (PDF) follows a normal (Gaussian) distribution:

$$p(z) = \frac{1}{\sqrt{2\pi}\sigma} e^{-\frac{(z-\mu)^2}{2\sigma^2}}$$



It affects every pixel in the image by adding or subtracting small random values. It typically arises during image acquisition due to sensor heat or poor illumination.
* **Salt and Pepper Noise:** Also known as impulse noise or data-drop noise. It randomly corrupts isolated pixels, forcing their values to either maximum intensity (white/salt) or minimum intensity (black/pepper). It is caused by malfunctioning pixel elements in camera sensors, memory transmission errors, or digitization flaws.

### 10. What are called median filters? Explain the operation of median filter.

A **median filter** is a non-linear spatial filter used primarily to reduce noise (especially effective against impulse/salt-and-pepper noise) while preserving sharp edges in an image.

**Operation:**

1. A sliding window (e.g., $3 \times 3$ or $5 \times 5$ matrix) moves over every pixel of the image sequentially.
2. The intensity values of all the pixels falling within the window are extracted and sorted in numerical ascending/descending order.
3. The center pixel value of the window is replaced by the **median value** of the sorted list.

> **Example:** For a window sequence: $[10, 12, 11, 255, 13, 9, 14, 11, 12]$, sorting gives: $[9, 10, 11, 11, \mathbf{12}, 12, 13, 14, 255]$. The center pixel is replaced with the median value `12`, stripping away the noisy peak `255`.

### 11. What is image averaging? Discuss histogram characteristics for dark, bright, and low-contrast images.

* **Image Averaging:** A spatial domain enhancement technique used to reduce random, zero-mean noise by averaging a set of $M$ noisy images $\{g_i(x,y)\}$ of the same scene:

$$\bar{f}(x,y) = \frac{1}{M} \sum_{i=1}^M g_i(x,y)$$



As $M$ increases, the variance of the noise decreases by a factor of $1/M$, leaving a clean image.

**Histogram Characteristics:**

* **Dark Image:** The components of the histogram are concentrated heavily on the **low-intensity (left) side** of the scale.
* **Bright Image:** The components are concentrated heavily on the **high-intensity (right) side** of the scale.
* **Low-Contrast Image:** The histogram is very narrow and clustered tightly around the **center** of the gray-level scale, indicating a lack of dynamic range.

### 12. Write the expression of laplacian filter of an image. What is bit plane slicing method?

The **Laplacian** is a derivative operator used to highlight sharp intensity transitions (edges) in an image. Its discrete expression for a 2D image $f(x,y)$ is:


$$\nabla^2 f(x,y) = [f(x+1,y) + f(x-1,y) + f(x,y+1) + f(x,y-1)] - 4f(x,y)$$


In matrix form, it is represented by the standard kernel:


$$\begin{bmatrix} 0 & 1 & 0 \\ 1 & -4 & 1 \\ 0 & 1 & 0 \end{bmatrix}$$

**Bit-Plane Slicing Method:**
An 8-bit image can be thought of as consisting of eight 1-bit planes, ranging from bit-plane 0 (Least Significant Bit - LSB) to bit-plane 7 (Most Significant Bit - MSB).

* **Function:** This method slices the image into these individual binary layers. The higher-order bits (planes 5 to 7) contain the majority of the visually significant structural data, while the lower-order bits contain fine details or noise. It is useful for image compression and steganography.

### 13. Contrast and compare spatial domain filtering and frequency domain filtering.

| Feature | Spatial Domain Filtering | Frequency Domain Filtering |
| --- | --- | --- |
| **Operation Principle** | Modifies pixels directly based on neighboring pixel values. | Modifies the Fourier transform of the image based on frequency components. |
| **Mathematical Basis** | Uses **Convolution** ($f(x,y) * h(x,y)$). | Uses **Multiplication** ($F(u,v) \cdot H(u,v)$). |
| **Tools Used** | Convolution masks/kernels ($3 \times 3$, $5 \times 5$, etc.). | Fast Fourier Transform (FFT) and frequency filters (Ideal, Butterworth). |
| **Computational Efficiency** | Highly efficient for small filter sizes. | Highly efficient for large filter sizes due to the FFT algorithm. |
| **Intuition** | Easier to understand visually. | More effective for complex patterns, periodic noise removal, and blur modeling. |

### 14. Explain what you understand about image histogram of a digital image.

An **image histogram** is a graphical representation of the frequency distribution of gray levels (or color intensities) in a digital image.

* The horizontal axis ($x$-axis) represents the distinct gray-level intensities ($0$ to $L-1$, typically $0$ to $255$).
* The vertical axis ($y$-axis) represents the total number of pixels possessing that specific intensity value.

Mathematically, it is defined as:


$$h(rk) = n_k$$


where $r_k$ is the $k$-th gray level and $n_k$ is the number of pixels in the image having gray level $r_k$.

**Significance:** It provides a snapshot of the image's overall contrast, brightness, and exposure quality, serving as the foundational metric for enhancement algorithms like Histogram Equalization.

### 15. Describe contrast stretching of an image. Difference between lossy and lossless transformation.

**Contrast Stretching:**
It is a linear transformation method used to expand the narrow dynamic range of an image's gray levels across the full available display spectrum (e.g., 0 to 255). It maps input intensities $(r_{min}, r_{max})$ to a wider range $(s_{min}, s_{max})$ using the transformation equation:


$$s = \frac{r - r_{min}}{r_{max} - r_{min}} \times (s_{max} - s_{min}) + s_{min}$$

**Difference between Lossy and Lossless Transformation/Compression:**

* **Lossless Transformation:** Reconstructs the exact original data from the compressed file without any degradation. No data is discarded. (e.g., PNG, Huffman coding, Run-Length Encoding).
* **Lossy Transformation:** Discards redundant or visually imperceptible information to achieve much higher compression ratios. The original data cannot be perfectly recovered. (e.g., JPEG, MPEG compression).

---

## Unit 5

### 16. What is homomorphic filtering? Setup the equation for this filter.

**Homomorphic filtering** is a frequency domain technique used to improve the appearance of an image by simultaneously normalizing illumination variations and increasing contrast. It handles images where illumination is non-uniform.

An image $f(x,y)$ is modeled as a product of illumination $i(x,y)$ (low frequencies) and reflectance $r(x,y)$ (high frequencies):


$$f(x,y) = i(x,y) \cdot r(x,y)$$

**Equation Setup Steps:**

1. Take the natural logarithm to make the components additive:

$$\ln[f(x,y)] = \ln[i(x,y)] + \ln[r(x,y)]$$


2. Apply the Fourier Transform (FFT):

$$F(u,v) = I(u,v) + R(u,v)$$


3. Apply a homomorphic filter function $H(u,v)$ that attenuates low frequencies and amplifies high frequencies:

$$G(u,v) = H(u,v) \cdot F(u,v) = H(u,v)I(u,v) + H(u,v)R(u,v)$$


4. Take the Inverse Fourier Transform ($IFFT$) and compute the exponential to return to the spatial domain:

$$g(x,y) = \exp[g_{\text{spatial}}(x,y)]$$



### 17. Difference between unconstrained and constrained restoration.

Image restoration aims to recover an original image $f$ from a degraded observation $g = Hf + \eta$ (where $H$ is degradation and $\eta$ is noise).

* **Unconstrained Restoration:** Minimizes the least-squares error between the observed and estimated image without any constraints regarding noise or smoothness.
* *Example:* **Inverse Filtering**. It completely ignores noise, leading to catastrophic noise amplification when values of $H(u,v)$ are close to zero.


* **Constrained Restoration:** Incorporates prior knowledge or constraints (such as noise power or image smoothness parameters) to control error amplification.
* *Example:* **Wiener Filtering** or Constrained Least Squares (CLS) filtering. It balances inverse degradation handling against noise minimization based on the signal-to-noise ratio.



---

## Unit 6

### 18. What is Hough transform and where it is used?

The **Hough Transform** is a feature extraction technique used to detect simple geometric shapes—such as lines, circles, or ellipses—within a digital image, even if the shapes are broken or corrupted by noise.

**Principle:** It maps points from the image space into a parameter space (Hough space). For example, a straight line represented as $y = mx + c$ can be converted to polar coordinates to avoid infinite slopes:


$$\rho = x \cos\theta + y \sin\theta$$


Each edge pixel in the image space votes for all possible $(\rho, \theta)$ combinations it could belong to. Accumulator cells with local maxima identify the parameter lines present in the image.

**Applications:**

* Detecting lanes in autonomous driving systems.
* Identifying barcode boundaries or industrial parts on assembly lines.
* Medical imaging for detecting circular structures like blood vessels or cells.

### 19. Difference between local and global thresholding.

Thresholding converts a grayscale image into a binary image based on a threshold $T$.

* **Global Thresholding:** A single, constant threshold value $T$ is calculated for the **entire image** based on global properties (like the total image histogram). A pixel becomes white if $f(x,y) > T$, otherwise black. It works well only when background illumination is perfectly uniform.
* **Local (Adaptive) Thresholding:** The threshold value $T(x,y)$ changes dynamically **across different regions** of the image. The value of $T$ for a pixel is computed based on the localized statistical properties (e.g., mean or median) of its small neighborhood window. It is ideal for images with uneven lighting or shadows.

### 20. Difference between region growing and split-and-merge techniques.

Both are region-based segmentation techniques, but they approach the problem from opposite directions:

* **Region Growing (Bottom-Up):** Starts with a set of "seed" pixels. It inspects neighboring pixels and appends them to the growing region if they satisfy predefined similarity criteria (like intensity or color). The process repeats until no more pixels match the criteria.
* **Split and Merge (Top-Down & Bottom-Up):** Starts with the **entire image** as a single region. If it does not satisfy a homogeneity criteria, it **splits** the region into four quadrants (using a quadtree structure). This continues recursively. Afterward, adjacent quadrants that are sufficiently similar are **merged** back together to form final segmented regions.

### 21. Define edge detection.

**Edge Detection** is an image segmentation technique that identifies and locates sharp discontinuities or rapid changes in pixel intensity within an image. These changes typically correspond to boundaries of objects, changes in depth, variations in scene illumination, or changes in material properties.

Mathematically, edges are detected by calculating first-order derivatives (Gradients like Sobel, Prewitt operators) to locate intensity peaks, or second-order derivatives (Laplacian, Canny) to find zero-crossings.

### 22. Explain Bi-linear interpolation method.

**Bilinear Interpolation** is a resampling method used to estimate the intensity value of a new pixel location during geometric modifications like scaling or rotation. It extends linear interpolation by working in two dimensions.

**Method:**
Instead of taking the value of the nearest pixel, it performs a weighted average using the **four closest surrounding pixels** in a $2 \times 2$ neighborhood.

1. First, it interpolates linearly along the horizontal direction ($x$-axis) between the top two pixels and the bottom two pixels.
2. Next, it interpolates vertically ($y$-axis) between the two newly calculated intermediate points to compute the final destination intensity. This yields much smoother results than nearest-neighbor interpolation, minimizing pixelation.
