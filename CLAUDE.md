# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

RNA-seq differential expression analysis project using R, Quarto, and DESeq2. Analyzes transcript-level quantification from Salmon to identify differentially expressed genes across timepoints (A, V1, V2) in aortic valve samples.

## Token-Policy

- Scanne NICHT automatisch das gesamte Repository.
- Arbeite bevorzugt mit einzelnen Dateien oder eingefügten Code-Ausschnitten.
- Wenn unklar ist, welche Datei relevant ist: erst nachfragen.
- Vermeide es, große Analyse-Skripte standardmäßig neu einzulesen.

## Pipeline Overview:
- Read in C:\Users\nn\Desktop\2025-13-10 RNAseq\code\DEanalysis\docs\pipeline_overview.md and document important changes to the code there

## Project Knowledge Architecture (WICHTIG)

Dieses Repository nutzt eine explizite Wissensstruktur.
Claude muss Ergebnisse immer diesen Dokumenttypen zuordnen.

### Zentrale Wissensdokumente

#### 1. PROJECT_STATUS.md (Pfad: ../../proj/PROJECT_STATUS.md)
Zweck:
- aktueller Stand
- Meilensteine
- To-dos
- Session-Handoffs

Claude soll:
- am Ende größerer Sessions eine kurze Status-Notiz vorschlagen.

---

#### 2. METHODS_AUDIT.md (Pfad: ../../meth/METHODS_AUDIT.md)
Zweck:
- Methodenbewertung
- Reviewer-Risiken
- Fixes
- Argumentationslinien

Claude soll:
- hier Audit-Ergebnisse, Kritikpunkte und Verbesserungen einsortieren,
- nicht in Ergebnisdokumente mischen.

---

#### 3. RESULTS_STORY.md (Pfad: ../../res/RESULTS_STORY.md)
Zweck:
- biologische Erzählung
- Paper-Rohbau

Claude soll:
- Methodenbegriffe vermeiden,
- Pathways biologisch interpretieren,
- Kernaussagen verdichten.

---

#### 4. METHODS_DECISIONS.md (Pfad: ../../meth/METHODS_DECISIONS.md)
Zweck:
- explizite Dokumentation aller Analyseentscheidungen

Claude soll:
- jede neue methodische Wahl hier als Decision/Reason/Risk/Mitigation formulieren.

---

### Bestehende Referenzdokumente

Claude soll diese als „Wissensbasis“ betrachten und NICHT neu erfinden:

- AUDIT_REPORT_Functional_Analysis.md  
- EXTREME_PVALUES_FAQ.md  
- pipeline_overview.md  
- PROJECT_HANDOFF.md  
- tavi_rnaseq_functional_analysis_summary.md  

---

### Arbeitsregel für Claude

Wenn neue Inhalte entstehen, sollen sie immer einer der Kategorien zugeordnet werden:

- Status → PROJECT_STATUS.md  
- Methodik → METHODS_AUDIT.md  
- Entscheidung → METHODS_DECISIONS.md  
- Biologie → RESULTS_STORY.md  
- Arbeitsweise / Prompts → PLAYBOOK.md  

Claude soll explizit sagen:
„Das gehört in …“

---

### Ziel dieser Struktur

- reproduzierbare Analyse  
- reviewer-sichere Argumentation  
- saubere Trennung von Code, Methodik, Biologie und Meta-Wissen  
- verlustfreie Nutzung von KI-generiertem Wissen

### Session-Abschluss-Regel (verbindlich)

Am Ende jeder inhaltlich produktiven Session soll Claude explizit liefern:

1. PROJECT_STATUS-Update (3–6 Bulletpoints)
2. Neue Decisions (für METHODS_DECISIONS.md)
3. Neue/geschärfte biologische Aussagen (für RESULTS_STORY.md)
4. Neue Reviewer-Risiken oder Fixes (für METHODS_AUDIT.md)

Format:
"Updates für PROJECT_STATUS.md:"
- ...

"Eintrag für METHODS_DECISIONS.md:"
- ...

usw.

### Priorität bei Zielkonflikten

Wenn es einen Konflikt gibt zwischen:
- schneller Antwort
- und methodischer / biologischer Korrektheit

ist immer zu priorisieren:
Korrektheit, Reproduzierbarkeit, Reviewer-Tauglichkeit.

