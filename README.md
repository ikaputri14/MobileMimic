# MobileMimic Cross-Domain Generalization Demo

A self-contained, reproducible example of training and evaluating a touch-based continuous authenticator on the **MobileMimic** dataset, checking whether a model trained the way any real deployed system would be trained (genuine user vs. random "zero-effort" impostors) holds up against a harder, more realistic adversary, mimicry attack.

This folder contains everything needed to run the demo yourself:

| File | Purpose |
|---|---|
| `cross_domain_generalization_demo.ipynb` | The notebook itself |
| `requirements.txt` | Exact Python package versions the notebook was built and tested against |
| `README.md` | This file |

You will additionally need the **raw MobileMimic CSV files**, downloaded separately from Figshare.

## Overview

Smartphones store and provide access to large volumes of sensitive personal information, making continuous, post-unlock authentication an active area of research. Behavioral biometrics that verifying identity from how a user touches and moves their phone, rather than a one-time password or fingerprint check offer a passive way to do this. A **targeted mimicry attacker** who has watched recorded video of a specific victim's swiping motion and deliberately tries to reproduce it is a hard adversary.

**MobileMimic** is a paired victim–attacker dataset with genuine baseline behavior from 23 victims, paired with real, video-informed mimicry attempts from 13 attackers who studied and imitated a specific victim. Both roles complete an identical structured protocol with every raw touch event (coordinates, pressure, contact size) and simultaneous device-orientation reading (pitch, roll, azimuth) logged individually as **18 raw fields per event**. The attacker–victim pairing is encoded directly in the file naming scheme, so the paired adversarial ground truth this dataset provides needs no separate annotation step.

The notebook in this folder derives a 49-feature, per-flick representation from those 18 raw fields or the **Dynamic Data** representation (touch-position/velocity/acceleration derivatives plus per-flick orientation statistics). 

This notebook demonstrates one concrete use of that pairing: training a reference SVM authenticator on zero-effort data alone, then evaluating that same model against a real mimicry attacker.

## Data Availability

The MobileMimic dataset is deposited on **Figshare**.

Once downloaded and extracted, point the notebook's `DATA_ROOT` variable at the folder containing the dataset's `victim/` and `attack/` subfolders.

**Data are anonymized.** All participant identifiers in the released files are generic codes (`V01`–`V23` for victims, `A01`–`A13` for attackers) with no real names or original device identifiers

## Citation

If you use this dataset or this reference implementation, please cite the dataset descriptor paper. Full author list and DOI will be added here once the paper and Figshare deposition are finalized:

```bibtex
@article{Putri2026,
  author = "Ika Putri and Yan-Qin Ni and Pratomo Adinegoro and Wei-Jen Wang and Chia-Yu Lin and Deron Liang",
  title = "{MobileMimic: Mobile Behavioral Biometrics Dataset of Mimickry Attacks}",
  year = "2026",
  month = "8",
  url = "https://figshare.com/articles/dataset/MobileMimic_Mobile_Behavioral_Biometrics_Dataset_of_Mimickry_Attacks/33320526",
  doi = "10.6084/m9.figshare.33320526.v1"
}
```

## License

See the dataset's Figshare record for the applicable license terms.
