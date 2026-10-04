This MATLAB App Designer program (`Project_FDTD1`) builds an interactive GUI application to simulate and visualize Maxwell's equations using the **Finite-Difference Time-Domain (FDTD)** method in both **1D** and **2D** spaces.

Here is a breakdown of what the code does:

---

### **1. User Interface (UI) Architecture**

* **Control Controls:** Includes dropdowns for mode selection (`1D Mode` vs. `2D Mode`), a list box to select materials, customizable spinners for custom relative permittivity ($\epsilon_r$) and permeability ($\mu_r$), and control buttons (`Run` / `Pause`).


* **Visualization Axes:**
* **UIAxes:** Displays real-time wave propagation dynamics.


* **UIAxes2:** Displays frequency-domain spectral analysis (Reflectance, Transmittance, and Total energy) updated via discrete Fourier transforms.





---

### **2. Material and Medium Selection**

The app configures optical and magnetic material properties based on user selection:

* **Standard Materials:** Defines preset permittivity ($\epsilon_r$) and permeability ($\mu_r$) values for Air, Water, Wood, Aluminum, Paper, Glass, $\text{SiO}_2$, Stainless Steel, and Graphite.


* **Multilayer Devices:** Configures 3-layer heterostructures (`Device 1`, `Device 2`, `Device 3`) combining distinct materials.


* **Custom Material:** Allows manual entry of $\epsilon_r$ and $\mu_r$ via the UI spinners.



---

### **3. Simulation Engines**

#### **A. 1D FDTD Mode**

* **Wave Generation:** Excites a Gaussian pulse source for electric ($E_y$) and magnetic ($H_x$) field components.


* **Discretization:** Sets up spatial resolution ($dz$) based on the maximum frequency ($f_{\text{max}} = 1\text{ GHz}$) and time resolution ($dt$) following the Courant stability condition.


* **Propagation & Boundaries:** Uses standard 1D leapfrog Yee-stepping updates for field components with Mur absorbing boundary conditions (ABC) at grid edges.


* **Visualization:** Plots dynamic 1D $E_y$ and $H_x$ wave profiles traveling through multi-region media boundaries.



#### **B. 2D TM$_z$ FDTD Mode**

* **Field Formulation:** Solves for transverse magnetic ($\text{TM}_z$) waves with $E_z$, $H_x$, and $H_y$ field matrices across a $120 \times 120$ spatial grid.


* **Target Geometries:** Positions physical scatterers inside the grid:


* A 3D cylindrical dielectric target for standard single materials.


* A 3D rectangular block for 3-layer multi-device setups.




* **Boundaries:** Uses 1st-Order Mur Absorbing Boundary Conditions (ABC) to minimize artificial reflections at domain edges.


* **Visualization:** Displays a live 3D surface mesh of $E_z$ (blue) and $H_x$ (red) fields propagating around the 3D target geometry.



---

### **4. Frequency Domain Analysis & Data Export**

* **Fourier Transform (FFT On-the-Fly):** Periodically computes frequency spectra using phase factors ($K = e^{-j 2 \pi f \Delta t}$) at sensor planes.


* **Reflectance & Transmittance:** Tracks reflected, transmitted, and total power ratios across $0 \text{ to } 1\text{ GHz}$.


* **Excel Data Output:** Automatically exports the resulting frequency, reflectance, transmittance, and total energy vectors into a timestamped Excel spreadsheet (`Data_1D_*.xlsx` or `Data_2D_*.xlsx`) when paused or finished.
