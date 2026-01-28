# Clinical Integration Analysis

Dieses Verzeichnis enthält die klinische Datenintegration für das TAVI RNA-seq Projekt.

## Struktur

```
clinical/
├── clinical_integration.qmd   # Haupt-Analysedokument (12-Schritte-Plan)
├── README.md                  # Diese Datei
└── (Output wird generiert in ../../res/clinical/)
```

## Abhängigkeiten

**WICHTIG:** Vor Ausführung von `clinical_integration.qmd`:

1. **DEanalysis.qmd** muss bis mindestens Chunk `deseq2-normalization` gelaufen sein
   - Erzeugt: `../../res/cache/sample_meta_deseq2.rds`

2. **GSVA-Analysen** in DEanalysis.qmd müssen abgeschlossen sein
   - Erzeugt: `../../res/cache/gsva_*.rds`

3. **Klinische Rohdaten** müssen verfügbar sein:
   - `../../dat/info_files/2026-01-03_clinical_data.csv`

## Workflow

### Phase 1: Setup (einmalig)

```r
# In RStudio: Öffne clinical_integration.qmd
# Führe Chunk "setup-packages" aus
```

### Phase 2: Data Preparation (Schritte 1-4)

```r
# Chunks ausführen:
# - step1-import-clinical
# - step2-variable-engineering
# - step3-join-metadata
# - step4-dropout-analysis
```

**Output:**
- `../../res/cache/clinical/sample_meta_clinical.rds`
- `../../res/cache/clinical/sample_meta_clinical_complete.rds`

### Phase 3: Feature Engineering (Schritte 5-7)

```r
# Chunks ausführen (eval=TRUE setzen):
# - step5-deconvolution (OPTIONAL)
# - step6-gsva-pathways
# - step7-delta-variables
```

**Output:**
- `../../res/cache/clinical/delta_data_clinical.rds`

### Phase 4: Analyses (Schritte 8-12)

```r
# Chunks ausführen (eval=TRUE setzen):
# - step8-table1
# - step9-primary-q1-ef-inflammation
# - step9-primary-q2-cad-ribosome
# - ... weitere Analysen
```

**Output:**
- `../../res/clinical/table1.csv`
- `../../res/clinical/primary_results.rds`
- `../../res/figures/clinical/*.png`

## Methodische Referenzen

Dieses Dokument implementiert den **12-Schritte-Plan** aus:
`../../meth/CLINICAL_INTEGRATION_REVIEW.md`

Basierend auf:
- Schmader et al. 2021 (BMC Cardiovasc Disord) — Baseline-Inflammation → TAVR-Outcomes
- Kuppe et al. 2024 (Circ Genom Precis Med) — Longitudinale Immunantwort
- Vestal et al. 2020 (BMC Bioinformatics) — MCMSeq für repeated measures

## Wichtige Parameter

In `clinical_integration.qmd`:

```r
params <- list(
  padj_cutoff = 0.05,
  min_n_per_group = 15,    # Minimum n für Interaktionen
  min_n_subgroup = 20,     # Minimum n für Subgruppen
  vif_threshold = 5,       # Kollinearitäts-Schwelle
  seed = 42
)
```

## Stop-Regeln

Das Dokument implementiert automatische Stop-Regeln:

- **Dropout >30%:** Warnungen bei Schritt 4
- **Zellenbesetzung <15:** Keine Interaktionsanalysen (Schritt 9)
- **VIF >5:** Warnung bei Kollinearität
- **Join-Rate <90%:** Warnung bei Schritt 3

## Troubleshooting

### "sample_meta nicht gefunden"
→ Erst `DEanalysis.qmd` bis Chunk `deseq2-normalization` laufen lassen

### "GSVA-Cache nicht gefunden"
→ Erst GSVA-Chunks in `DEanalysis.qmd` ausführen

### "Clinical CSV nicht gefunden"
→ Pfad prüfen: `../../dat/info_files/2026-01-03_clinical_data.csv`

### Encoding-Fehler (prä → pr�)
→ Wird automatisch in Schritt 1 gehandhabt (UTF-8 Konvertierung)

## Nächste Schritte

1. ✅ `clinical_integration.qmd` erstellt
2. ⏳ Führe Schritte 1-4 aus (Data Prep)
3. ⏳ Setze `eval=TRUE` für Schritte 5-7 (Feature Engineering)
4. ⏳ Implementiere verbleibende Primary Analyses (Schritte 9-12)

## Kontakt

Fragen zur Implementierung → siehe `CLINICAL_INTEGRATION_REVIEW.md` (Section 5: Implementierungsplan)
