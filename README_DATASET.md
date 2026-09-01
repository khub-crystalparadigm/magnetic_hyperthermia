# README: Curated Dataset on Magnetic Hyperthermia Therapy (MHT), Nanoparticle Properties, and Specific Absorption Rate (SAR)

## Overview
This dataset contains comprehensive, extracted, and processed data compiled from peer-reviewed literature focusing on **Magnetic Hyperthermia Therapy (MHT)** using magnetic nanoparticles (MNPs). The dataset is structured for materials informatics, machine learning modeling (e.g., predicting Specific Absorption Rate - SAR), and comparative bibliometric analyses of magnetic nanomaterials.

- **Total Records / Samples:** 1,548 entries (across 183 unique source publications) [cite: source]
- **Data Source:** Curated from peer-reviewed research publications in materials science, nanotechnology, and biomedicine [cite: source].
- **File Format:** Excel workbook (`.xlsx`) / Comma-Separated Values (`.csv`)

---

## Data Extraction & Curation Strategy
The literature-derived dataset was assembled through the following sequential steps [cite: source]:

1. **Step 1 - Literature Search:** Boolean queries combining material terms (Nanoparticle, Iron oxide, Ferrite), magnetic-property terms (Superparamagnet, Magnet), and application terms (Hyperthermia, Heat) were run across ScienceDirect, Google Scholar, MDPI, and IEEE Xplore for publications from 2000–2026 [cite: source].
2. **Step 2 - Initial Screening:** Duplicate records and studies unrelated to magnetic hyperthermia were removed, narrowing over 500 initial records to approximately 300 candidate papers [cite: source].
3. **Step 3 - Eligibility Assessment:** Full-text review retained only studies reporting experimentally determined SAR values with sufficient composition, physicochemical, magnetic, and experimental-condition detail, resulting in 183 unique source publications [cite: source].
4. **Step 4 - Manual Data Collection:** Data points were extracted directly from text, tables, and figures. Values available only in graphical form were digitized using WebPlotDigitizer [cite: source].
5. **Step 5 - No-Assumption Curation:** Only explicitly reported or directly extractable values were entered; missing information was left blank rather than estimated [cite: source].
6. **Step 6 - Row Construction:** Each distinct experimental condition (composition, particle characteristics, applied field, frequency, concentration, etc.) was recorded as a separate row, so a single publication could contribute multiple rows [cite: source].
7. **Step 7 - Compositional Encoding:** Chemical formulae were converted into stoichiometric fractions for Ca, Co, Cu, Fe, Ga, Gd, Mg, Mn, Nd, Ni, Sn, Tb, and Zn; Fe was excluded as a dopant variable since it is stoichiometrically dependent on the other elements [cite: source].
8. **Step 8 - Unit Harmonization:** Measurements were standardized to consistent units—nanoparticle dimensions in $	ext{nm}$, saturation magnetization in $	ext{emu g}^{-1}$, coercivity and field strength in $	ext{Oe}$, frequency in $	ext{kHz}$, concentration in $	ext{mg mL}^{-1}$, and SAR in $	ext{W g}^{-1}$ [cite: source].
9. **Step 9 - Range and Boundary Handling:** Reported value ranges were converted to their statistical mean; qualitative or inequality-based values (e.g., '>', '<') were translated into fixed numerical approximations [cite: source].
10. **Step 10 - Final Dataset Assembly:** The curated dataset was compiled into 37 columns—2 metadata fields (serial number, DOI), 34 input features, and 1 target column (SAR)—totaling 1,548 records [cite: source].

---

## Dataset Structure & Column Descriptions

The dataset includes physical, chemical, magnetic, and therapeutic parameters of synthesized magnetic nanoparticles. Below is the complete data dictionary explaining each column:

| Column Name | Data Type | Description / Definition | Unit / Scale |
| :--- | :--- | :--- | :--- |
| `-` | Integer | Index / Entry identifier | Numeric |
| `DOI` | String | Digital Object Identifier of the source research paper | Text |
| `f_avg_core_width_nm` | Float | Average core width / diameter of the magnetic nanoparticle | Nanometers ($	ext{nm}$) |
| `f_Ms_emu_g_MNP` | Float | Saturation Magnetization ($M_s$) of the magnetic nanoparticle | $	ext{emu g}^{-1}$ |
| `f_Hc_Oe` | Float | Coercive field ($H_c$) | Oersteds ($	ext{Oe}$) |
| `c_core_composition` | String | Chemical composition of the nanoparticle core (e.g., $	ext{Fe}_3	ext{O}_4$, spinel ferrites, doped ferrites) | Chemical formula |
| `is_doped` | Integer | Binary indicator for dopant presence (1 = Doped, 0 = Undoped) | Binary (0, 1) |
| `c_dopant_element` | String | Specific dopant element(s) introduced into the core matrix (e.g., $	ext{Gd}$, $	ext{Nd}$, $	ext{Tb}$) | Element symbol |
| `f_is_coated` | Integer | Binary indicator for surface coating (1 = Coated, 0 = Bare) | Binary (0, 1) |
| `f_is_organic` | Integer | Binary indicator if coating is organic (e.g., polymers, surfactants) | Binary (0, 1) |
| `f_is_inorganic` | Integer | Binary indicator if coating is inorganic (e.g., silica, gold) | Binary (0, 1) |
| `f_is_composite_coating` | Integer | Binary indicator for multi-layer or composite coatings | Binary (0, 1) |
| `c_coating` | String | Specific coating material name (e.g., Chitosan, PEG, Silica, Dextran) | Text |
| `f_H_Oe` | Float | Applied alternating magnetic field strength ($H$) | Oersteds ($	ext{Oe}$) |
| `f_FCY_kHz` | Float | Frequency ($f$) of the alternating magnetic field | Kilohertz ($	ext{kHz}$) |
| `f_conc_MNP_mg_mL` | Float | Concentration of magnetic nanoparticles in the suspension medium | $	ext{mg mL}^{-1}$ |
| `c_shape_type` | String | Morphological shape of the nanoparticles (e.g., spherical, cubic, octahedral) | Text |
| `c_magnetic_phase` | String | Magnetic behavior/phase (e.g., superparamagnetic, ferromagnetic) | Text |
| `f_SAR_W_g` | Float | Specific Absorption Rate (SAR) — target therapeutic heating output | Watts per gram ($	ext{W g}^{-1}$) |
| `f_avg_core_sd_nm _BOTH` | Float | Standard deviation or error margin associated with core size measurements | Nanometers ($	ext{nm}$) |
| `f_area_core_estimated_nm2` | Float | Estimated surface area of the nanoparticle core | Square nanometers ($	ext{nm}^2$) |
| `f_volume_core_estimated_nm3` | Float | Estimated volume of the nanoparticle core | Cubic nanometers ($	ext{nm}^3$) |
| `f_area_volume_ratio` | Float | Surface-area-to-volume ratio of the core | $	ext{nm}^{-1}$ |
| `f_dopant_ratio` | Float | Atomic or stoichiometric ratio of the dopant element | Ratio (0 - 1) |
| `Ca_comp` to `Zn_comp` | Float | Atomic composition ratios for specific constituent transition metals and rare-earth elements ($	ext{Ca}, 	ext{Co}, 	ext{Cu}, 	ext{Fe}, 	ext{Ga}, 	ext{Gd}, 	ext{Mg}, 	ext{Mn}, 	ext{Nd}, 	ext{Ni}, 	ext{Sn}, 	ext{Tb}, 	ext{Zn}$) | Stoichiometric value |

---

## Usage & License
- **License:** Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Citation:** If you use this dataset in your research, please cite the corresponding Zenodo record and associated research publication.

## Contact
For questions, feedback, or collaborations regarding this dataset, please reach out to the corresponding research group repository maintainers.
