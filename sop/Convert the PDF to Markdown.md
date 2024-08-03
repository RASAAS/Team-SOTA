
### Tools install

Activate the Python environment through **Anaconda Navigator** or **Anaconda PowerShell Prompt**:

```
conda activate python
```

Install [marker](https://github.com/VikParuchuri/marker), keep default settings if the local machine is capable.

The installation will be located in `C:\apps\anaconda\envs\python311\Lib\site-packages\marker`, if Python environment is created by anaconda.

### Preparation

Prepare an output files folder (and/or its subfolders), such as:

`C:\apps\marker\md`, 
`C:\apps\marker\md\research-001`, `C:\apps\marker\md\research-002`...

### Convert

Convert PDF file(s) to .md using the following commands

#### Single file convert:

`marker_single C:\apps\marker\pdf\A-Head-to-Head-Comparison.pdf C:\apps\marker\md\research-001 --batch_multiplier 2 --max_pages 10 --langs English`

- `--batch_multiplier` is how much to multiply default batch sizes by if you have extra VRAM. Higher numbers will take more VRAM, but process faster. Set to 2 by default. The default batch sizes will take ~3GB of VRAM.
- `--max_pages` is the maximum number of pages to process. Omit this to convert the entire document.
- `--langs` is a comma separated list of the languages in the document, for OCR

#### Multiple files convert:

`marker /path/to/input/folder /path/to/output/folder --workers 10 --max 10 --metadata_file /path/to/metadata.json --min_length 10000`

- `--workers` is the number of pdfs to convert at once. This is set to 1 by default, but you can increase it to increase throughput, at the cost of more CPU/GPU usage. Parallelism will not increase beyond `INFERENCE_RAM / VRAM_PER_TASK` if you're using GPU.
- `--max` is the maximum number of pdfs to convert. Omit this to convert all pdfs in the folder.
- `--min_length` is the minimum number of characters that need to be extracted from a pdf before it will be considered for processing. If you're processing a lot of pdfs, I recommend setting this to avoid OCRing pdfs that are mostly images. (slows everything down)
- `--metadata_file` is an optional path to a json file with metadata about the pdfs. If you provide it, it will be used to set the language for each pdf. If not, `DEFAULT_LANG` will be used. The format is:
```
{
  "pdf1.pdf": {"languages": ["English"]},
  "pdf2.pdf": {"languages": ["Spanish", "Russian"]},
  ...
}
```

Find your .md files in the output folder(s)