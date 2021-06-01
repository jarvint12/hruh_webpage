1. Original instructions can be found from /csc/mustjoki/rnaseq/staging/README
2. Unlike with GATK pipeline, there is no script to making configuration file. However, the structure can be seen on the table below.
3. Run the script with
  1. grun.py -n rseq-XXX -q seq_hugemem2.q -c "/apps/perl/bin/perl /csc/mustjoki2/bioinformatics/transcriptome/src/2.8/star_pipeline.pm --file /path/to/configure.txt --execute --queue seq_hugemem2.q"
  2. grun.py -n rseq-XXX -q seq_hugemem2.q -c "/apps/perl/bin/perl /csc/mustjoki2/bioinformatics/transcriptome/src/2.8/star_pipeline.pm --file /path/to/configure.txt --fusion=0 -gatk=0 --execute --queue seq_hugemem2.q"
4. Force remove analysis folders grep OBS rseq_prometheus.3.ER | perl -p -e 's/^.* folder/rm -rf /g' | perl -p -e 's/for reruns//g' | sh
5. Check results with /apps/perl/bin/perl /csc/mustjoki2/bioinformatics/transcriptome/src/2.8/spipe_check_results.pm /path/to/configure.txt
6. Produce quality data with /apps/perl/bin/perl /csc/mustjoki2/bioinformatics/transcriptome/src/2.8/spipe_quality_report.pm short quick /path/to/configure.txt
...
