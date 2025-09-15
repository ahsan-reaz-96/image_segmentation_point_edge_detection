🤦‍♀️🤦‍♀️🤦‍♀️How to detect a point:
A point (or blob) = a single pixel or a very small region that is much brighter/darker than its neighbors (e.g. a dot, speck, or small bright spot). The general idea: preprocess → compute a response that highlights points → threshold → filter/locate → (optionally) refine and display.
👍Method A — Simple kernel (Laplacian-like) — easy and fast
Steps:
🎈 Load & convert to grayscale.
🎈(Optional) Denoise with small Gaussian blur.
🎈Convolve with a point kernel (e.g. [-1 -1 -1; -1 8 -1; -1 -1 -1]).
🎈Take absolute value → threshold to get candidate points.
🎈Filter by connected-component area and compute centroids.
🎈(Optional) refine centroid positions (sub-pixel).
🎈Visualize / overlay.
👍Method B — Blob detector (OpenCV SimpleBlobDetector) — robust & parameterized
Good when blobs vary a bit and you want built-in filters for area, circularity, convexity.
👍Method C — DoG / LoG (scale-space) — multi-scale point detection
If points have varying sizes, use Difference-of-Gaussian (DoG) or Laplacian-of-Gaussian (LoG) and detect local maxima across scales.
🔑 What this does:
DoG (manual): subtracts two Gaussian blurred versions → points appear bright.
LoG (blob_log): more robust, finds blobs at multiple scales.


Red circles = DoG blobs.

Green circles = LoG blobs.
