# Real-Time SVD Clutter Filtering using Preconditioning
Corresponding paper to the following presentation at IUS 2025.

📄 Talk/paper: [Real-Time SVD Clutter Filtering Using Preconditioning](https://github.com/sebftw/Preconditioned-SVD/blob/main/paper.pdf) (Id: 2569) 

🗓️ Session: Tuesday, Sept. 16, 15:07 - 15:30, MIS: Microvascular Imaging.

📍 Location: Kinepolis - Room 12

Authors: Sebastian Kazmarek Præsius (me), Kees Joost Batenburg, Jørgen Arendt Jensen.

## Abstract
Singular value decomposition (SVD) filtering is used in super-resolution and power-Doppler imaging to separate blood flow from the surrounding tissue signals. 
However, computing the singular vectors is time-consuming, limiting the ability to use the filter for live imaging.


It is hypothesized that the vectors that were computed for the previous video frame can be used as a starting point for the calculation of the next frame’s vectors, to allow real-time SVD-filtered power-Doppler imaging at a 417 images/s rate.


Every image was filtered using the neighboring 401 frames, and to speed up this sliding-window SVD processing, the singular vectors were found by eigendecomposing a temporal covariance matrix.
The eigendecomposition iteratively diagonalizes the input matrix, so instead of starting from scratch, the previous frame’s vectors were used to precondition (approximately diagonalize) the matrix and allow the next set of vectors to be found in fewer iterations. 
Batches of 32 frames were computed in parallel to use a graphics processing unit (GPU) more effectively, and the most recent set of vectors was used to precondition the batched eigendecomposition.
A GeForce RTX 4090 GPU carried out the processing for in vivo rat kidney data, acquired at a 417 Hz rate with a 10 MHz probe.

The resulting rate for the eigendecomposition was 1120 Hz, which was made 60% faster through preconditioning.
The imaging rate was 640 Hz after including all processing steps (RF data transfer, beamforming, motion correction, and SVD filtering). Thus, SVD-filtered power-Doppler imaging was performed in real-time using preconditioning, allowing live blood flow imaging at the bedside.
