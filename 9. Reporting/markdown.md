# OSCP Report Using markdown

## Sources
[noraj Report Template](https://github.com/noraj/OSCP-Exam-Report-Template-Markdown)

## Installation

1. Install required Libraries
```console
apt install texlive-latex-recommended texlive-fonts-extra texlive-latex-extra pandoc p7zip-full
```
2. Download eisvogel template from [eisvogel github](https://github.com/Wandmalfarbe/pandoc-latex-template#installation)
3. unzip downloaded file and move to `/usr/share/pandoc/data/templates/`
4. Edit `src/OSCP-exam-report-template_whoisflynn_v3.2.md`
5. Generate pdf using ruby script `ruby generate.rb`