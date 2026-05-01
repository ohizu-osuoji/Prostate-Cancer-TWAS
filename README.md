# Prostate-Cancer-TWAS
Tissue-level indicators of prostate cancer susceptibility using multi-ancestry Transcriptome-Wide Association Study (TWAS)

#####TiWASavage -- OH1deULTIMATE PRESENTS
#####from the base -- you want to conda activate imlabtools because that gives you the correct python environment

  conda activate imlabtools
  
####Then you need to do some kind of harmonizing on the data -- start by assigning variables to shorten paths in the commands below -- keep as is, run in RStudio Terminal 
  GWAS_TOOLS=/home/wheelerlab3/summary-gwas-imputation/src
  METAXCAN=/usr/local/bin/MetaXcan_software
  DATA=/home/wheelerlab3/mets-sleep/data
  
  #### Harmonize sumstats to predixcan models (run once) -- pay attention to the input values (gwas file, sample size, cases)
  /usr/bin/python $GWAS_TOOLS/gwas_parsing.py \
  -gwas_file /home/ohizu/OH1deULTIMATE/ohizu_THESIS/GCST90274713.h.tsv.gz \
  -snp_reference_metadata $DATA/reference_panel_1000G/variant_metadata.txt.gz METADATA \
  -output_column_map rsid rsid \
  -output_column_map other_allele non_effect_allele \
  -output_column_map effect_allele effect_allele \
  -output_column_map beta effect_size \
  -output_column_map standard_error standard_error \
  -output_column_map p_value pvalue \
  -output_column_map chromosome chromosome \
  --chromosome_format \
  -output_column_map base_pair_location position \
  -output_column_map effect_allele_frequency effect_allele_frequency \
  --insert_value sample_size 944762 --insert_value n_cases 156319 \
  -output_order rsid panel_variant_id chromosome position effect_allele non_effect_allele effect_allele_frequency pvalue effect_size standard_error sample_size n_cases \
  -output NEWhg38_SPx_GCST90274713.h_sumstats.tsv.gz
  
###Then you can actually run SPrediXcan
  ####TISSUE LEVEL // WAVY LEVEL
  
  ####. ADIPOSE SUBCUTANEOUS
  /usr/bin/python $METAXCAN/SPrediXcan.py \
  --gwas_file NEWhg38_SPx_GCST90274713.h_sumstats.tsv.gz \
  --snp_column panel_variant_id \
  --effect_allele_column effect_allele \
  --non_effect_allele_column non_effect_allele \
  --beta_column effect_size \
  --se_column standard_error \
  --model_db_path /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Adipose_Subcutaneous.db \
  --covariance /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Adipose_Subcutaneous.txt.gz \
  --keep_non_rsid \
  --additional_output \
  --model_db_snp_key varID \
  --throw \
  --output_file hg38_TissueSPx_GCST90274713.h_MASHRxADIPOSExSUBCUTANEOUS.csv
  
  ####  ADIPOSE VISCERAL OMENTUM
   /usr/bin/python $METAXCAN/SPrediXcan.py \
  --gwas_file NEWhg38_SPx_GCST90274713.h_sumstats.tsv.gz \
  --snp_column panel_variant_id \
  --effect_allele_column effect_allele \
  --non_effect_allele_column non_effect_allele \
  --beta_column effect_size \
  --se_column standard_error \
  --model_db_path /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Adipose_Visceral_Omentum.db \
  --covariance /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Adipose_Visceral_Omentum.txt.gz \
  --keep_non_rsid \
  --additional_output \
  --model_db_snp_key varID \
  --throw \
  --output_file hg38_TissueSPx_GCST90274713.h_MASHRxADIPOSExVISCERALxOMENTUM.csv
  
  #### ADRENAL
  /usr/bin/python $METAXCAN/SPrediXcan.py \
  --gwas_file hg38_SPx_GCST90274713.h_sumstats.tsv.gz \
  --snp_column panel_variant_id \
  --effect_allele_column effect_allele \
  --non_effect_allele_column non_effect_allele \
  --beta_column effect_size \
  --se_column standard_error \
  --model_db_path /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Adrenal_Gland.db \
  --covariance /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Adrenal_Gland.txt.gz \
  --keep_non_rsid \
  --additional_output \
  --model_db_snp_key varID \
  --throw \
  --output_file hg38_TissueSPx_GCST90274713.h_MASHRxADRENAL.csv
  
  #### KIDNEY CORTEX
  /usr/bin/python $METAXCAN/SPrediXcan.py \
  --gwas_file hg38_SPx_GCST90274713.h_sumstats.tsv.gz \
  --snp_column panel_variant_id \
  --effect_allele_column effect_allele \
  --non_effect_allele_column non_effect_allele \
  --beta_column effect_size \
  --se_column standard_error \
  --model_db_path /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Kidney_Cortex.db \
  --covariance /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Kidney_Cortex.txt.gz \
  --keep_non_rsid \
  --additional_output \
  --model_db_snp_key varID \
  --throw \
  --output_file hg38_TissueSPx_GCST90274713.h_MASHRxKIDNEYxCORTEX.csv
  
  #### LIVER
  /usr/bin/python $METAXCAN/SPrediXcan.py \
  --gwas_file hg38_SPx_GCST90274713.h_sumstats.tsv.gz \
  --snp_column panel_variant_id \
  --effect_allele_column effect_allele \
  --non_effect_allele_column non_effect_allele \
  --beta_column effect_size \
  --se_column standard_error \
  --model_db_path /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Liver.db \
  --covariance /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Liver.txt.gz \
  --keep_non_rsid \
  --additional_output \
  --model_db_snp_key varID \
  --throw \
  --output_file hg38_TissueSPx_GCST90274713.h_MASHRxLIVER.csv
  
  #### TIBIAL NERVE
  /usr/bin/python $METAXCAN/SPrediXcan.py \
  --gwas_file hg38_SPx_GCST90274713.h_sumstats.tsv.gz \
  --snp_column panel_variant_id \
  --effect_allele_column effect_allele \
  --non_effect_allele_column non_effect_allele \
  --beta_column effect_size \
  --se_column standard_error \
  --model_db_path /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Nerve_Tibial.db \
  --covariance /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Nerve_Tibial.txt.gz \
  --keep_non_rsid \
  --additional_output \
  --model_db_snp_key varID \
  --throw \
  --output_file hg38_TissueSPx_GCST90274713.h_MASHRxNERVExTIBIAL.csv
  
  #### PANCREAS
  /usr/bin/python $METAXCAN/SPrediXcan.py \
  --gwas_file hg38_SPx_GCST90274713.h_sumstats.tsv.gz \
  --snp_column panel_variant_id \
  --effect_allele_column effect_allele \
  --non_effect_allele_column non_effect_allele \
  --beta_column effect_size \
  --se_column standard_error \
  --model_db_path /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Pancreas.db \
  --covariance /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Pancreas.txt.gz \
  --keep_non_rsid \
  --additional_output \
  --model_db_snp_key varID \
  --throw \
  --output_file hg38_TissueSPx_GCST90274713.h_MASHRxPANCREAS.csv
  
  ##### PITUITARY
  /usr/bin/python $METAXCAN/SPrediXcan.py \
  --gwas_file hg38_SPx_GCST90274713.h_sumstats.tsv.gz \
  --snp_column panel_variant_id \
  --effect_allele_column effect_allele \
  --non_effect_allele_column non_effect_allele \
  --beta_column effect_size \
  --se_column standard_error \
  --model_db_path /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Pituitary.db \
  --covariance /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Pituitary.txt.gz \
  --keep_non_rsid \
  --additional_output \
  --model_db_snp_key varID \
  --throw \
  --output_file hg38_TissueSPx_GCST90274713.h_MASHRxPITUITARY.csv
  
  ##### PROSTATE
  /usr/bin/python $METAXCAN/SPrediXcan.py \
  --gwas_file hg38_SPx_GCST90274713.h_sumstats.tsv.gz \
  --snp_column panel_variant_id \
  --effect_allele_column effect_allele \
  --non_effect_allele_column non_effect_allele \
  --beta_column effect_size \
  --se_column standard_error \
  --model_db_path /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Prostate.db \
  --covariance /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Prostate.txt.gz \
  --keep_non_rsid \
  --additional_output \
  --model_db_snp_key varID \
  --throw \
  --output_file hg38_TissueSPx_GCST90274713.h_MASHRxPROSTATE.csv
  
  #### SPLEEN
  /usr/bin/python $METAXCAN/SPrediXcan.py \
  --gwas_file hg38_SPx_GCST90274713.h_sumstats.tsv.gz \
  --snp_column panel_variant_id \
  --effect_allele_column effect_allele \
  --non_effect_allele_column non_effect_allele \
  --beta_column effect_size \
  --se_column standard_error \
  --model_db_path /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Spleen.db \
  --covariance /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Spleen.txt.gz \
  --keep_non_rsid \
  --additional_output \
  --model_db_snp_key varID \
  --throw \
  --output_file hg38_TissueSPx_GCST90274713.h_MASHRxSPLEEN.csv
  
  #### TESTIS
  /usr/bin/python $METAXCAN/SPrediXcan.py \
  --gwas_file hg38_SPx_GCST90274713.h_sumstats.tsv.gz \
  --snp_column panel_variant_id \
  --effect_allele_column effect_allele \
  --non_effect_allele_column non_effect_allele \
  --beta_column effect_size \
  --se_column standard_error \
  --model_db_path /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Testis.db \
  --covariance /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Testis.txt.gz \
  --keep_non_rsid \
  --additional_output \
  --model_db_snp_key varID \
  --throw \
  --output_file hg38_TissueSPx_GCST90274713.h_MASHRxTESTIS.csv
  
  #### THYROID
  /usr/bin/python $METAXCAN/SPrediXcan.py \
  --gwas_file hg38_SPx_GCST90274713.h_sumstats.tsv.gz \
  --snp_column panel_variant_id \
  --effect_allele_column effect_allele \
  --non_effect_allele_column non_effect_allele \
  --beta_column effect_size \
  --se_column standard_error \
  --model_db_path /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Thyroid.db \
  --covariance /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Thyroid.txt.gz \
  --keep_non_rsid \
  --additional_output \
  --model_db_snp_key varID \
  --throw \
  --output_file hg38_TissueSPx_GCST90274713.h_MASHRxTHYROID.csv
  
  #### WHOLE BLOOD
  /usr/bin/python $METAXCAN/SPrediXcan.py \
  --gwas_file hg38_SPx_GCST90274713.h_sumstats.tsv.gz \
  --snp_column panel_variant_id \
  --effect_allele_column effect_allele \
  --non_effect_allele_column non_effect_allele \
  --beta_column effect_size \
  --se_column standard_error \
  --model_db_path /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Whole_Blood.db \
  --covariance /home/wheelerlab3/Data/predictdb_models/mashr/mashr_Whole_Blood.txt.gz \
  --keep_non_rsid \
  --additional_output \
  --model_db_snp_key varID \
  --throw \
  --output_file hg38_TissueSPx_GCST90274713.h_MASHRxWHOLExBLOOD.csv
 
####SINGLE-CELL
  
  
  
  
  
  
  /usr/bin/python $METAXCAN/SPrediXcan.py \
  --gwas_file hg38_SPx_GCST90274713.h_sumstats.tsv.gz \
  --snp_column panel_variant_id \
  --effect_allele_column effect_allele \
  --non_effect_allele_column non_effect_allele \
  --beta_column effect_size \
  --se_column standard_error \
  --model_db_path /home/wheelerlab3/Data/predictdb_models/scPrediXcan_models/l-ctPred_models_for_immune_cell_types_from_OneK1K_dataset/peripheral_blood_mononuclear_cell.db \
  --covariance /home/wheelerlab3/Data/predictdb_models/scPrediXcan_models/l-ctPred_models_for_immune_cell_types_from_OneK1K_dataset/peripheral_blood_mononuclear_cell_covariances.txt.gz \
  --keep_non_rsid \
  --additional_output \
  --model_db_snp_key varID \
  --throw \
  --output_file hg38_SPx_GCST90274713.h_PeripheralxBloodxSC.csv
  
  /usr/bin/python $METAXCAN/SPrediXcan.py \
  --gwas_file hg38_SPx_GCST90274713.h_sumstats.tsv.gz \
  --snp_column panel_variant_id \
  --effect_allele_column effect_allele \
  --non_effect_allele_column non_effect_allele \
  --beta_column effect_size \
  --se_column standard_error \
  --model_db_path /home/wheelerlab3/Data/predictdb_models/scPrediXcan_models/l-ctPred_models_for_immune_cell_types_from_OneK1K_dataset/plasmablast.db \
  --covariance /home/wheelerlab3/Data/predictdb_models/scPrediXcan_models/l-ctPred_models_for_immune_cell_types_from_OneK1K_dataset/plasmablast_covariances.txt.gz \
  --keep_non_rsid \
  --additional_output \
  --model_db_snp_key varID \
  --throw \
  --output_file hg38_SPx_GCST90274713.h_PlasmablastxSC.csv
  
  /usr/bin/python $METAXCAN/SPrediXcan.py \
  --gwas_file hg38_SPx_GCST90274713.h_sumstats.tsv.gz \
  --snp_column panel_variant_id \
  --effect_allele_column effect_allele \
  --non_effect_allele_column non_effect_allele \
  --beta_column effect_size \
  --se_column standard_error \
  --model_db_path /home/wheelerlab3/Data/predictdb_models/scPrediXcan_models/l-ctPred_models_for_immune_cell_types_from_OneK1K_dataset/platelet.db \
  --covariance /home/wheelerlab3/Data/predictdb_models/scPrediXcan_models/l-ctPred_models_for_immune_cell_types_from_OneK1K_dataset/platelet_covariances.txt.gz \
  --keep_non_rsid \
  --additional_output \
  --model_db_snp_key varID \
  --throw \
  --output_file hg38_SPx_GCST90274713.h_PlateletxSC.csv
  
  
####NOW IT'S TIME TO ORGANIZE -- ASAKE LEVEL 
  ##### First you need to specify the working directory from within the console
  setwd("/home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage")
  #### Then you need to load in the libraries
  library(data.table)
  library(ggplot2)
  library(qqman)
  library(locuszoomr)
  library(EnsDb.Hsapiens.v75)
  library(MetBrewer)
  library(ggrepel)
  library(dplyr)
  
  #### Next you need to define the tissues -- Make sure the tissue name matches the designation you gave it in the output file
  Tissues <- list("ADIPOSExSUBCUTANEOUS", "ADIPOSExVISCERALxOMENTUM", "ADRENAL", "KIDNEYxCORTEX",
                  "LIVER", "NERVExTIBIAL", "PANCREAS",
                  "PITUITARY", "PROSTATE", "SPLEEN",
                  "TESTIS", "THYROID", "WHOLExBLOOD")
  
  ####After that it's time to make a loopty loop
  Total <- data.frame()
  
  for (x in Tissues) {
    path <- paste("hg38_TissueSPx_GCST90274713.h_MASHRx", x, ".csv", sep="")
    message("Reading: ", path)  # prints progress so you can track it
    Tissue <- data.table::fread(path, header = TRUE, sep = ",")
    Tissue <- mutate(Tissue, gene = strtrim(gene, 15)) %>%
      mutate(tissue = x)
    Total <- rbind(Total, Tissue)
  }
  
  ####Once you make the loop you can sort by pvalue
      Total <- arrange(Total, pvalue)
      
  ####Then you can run these commands to make sure everything looks okay
      dim(Total)
      head(Total)
      table(Total$tissue)
      
  ####If everything looks fine you can now save the master file
      data.table::fwrite(Total, "Tissue_SPrediXCan_GCST90274713_AllTissues_Total.csv", append = FALSE, quote = "auto", sep = ",")
      
#####So now you have made the master file -- IT'S TIME TO PLOT
      
      ####Define the string concatenation helper
      "%&%" = function(a,b) paste(a,b,sep="")
      
      ####Load the gene annotation file
      gene_anno <- read.table("gencode38_geneid-to-name.txt", sep = ",", header = TRUE)
      
      ####Filter out chrM and chrY
      gene_anno <- gene_anno[gene_anno$chr != "chrM", ]
      gene_anno <- gene_anno[gene_anno$chr != "chrY", ]
      
      ####Create the chr_pos column
      gene_anno$chr_pos <- ifelse(gene_anno$chr %in% as.character(1:22), as.numeric(gene_anno$chr), NA)
      gene_anno <- gene_anno %>% mutate(chr_pos = ""%&% gene_anno$chr %&%":"%&% gene_anno$start)
      
      ####Trim gene IDs in gene_anno to 15 characters (critical fix — without this the join will return zero matches)
      gene_anno$gene_id <- strtrim(gene_anno$gene_id, 15)
      head(gene_anno$gene_id)  # confirm decimals are gone
      
      #####Read in your master file
      Total <- data.table::fread("Tissue_SPrediXCan_GCST90274713_AllTissues_Total.csv", header = TRUE, sep = ",")
      
      #####Confirm gene IDs in Total look right
      head(Total$gene)
      sum(Total$gene %in% gene_anno$gene_id)  # should be greater than 0
      
      
      #####Drop unnecessary columns
      gwas_file <- Total %>% select(-c(pred_perf_pval, pred_perf_r2, pred_perf_qval))
      
      #####Trim gene IDs in gwas_file
      gwas_file <- mutate(gwas_file, gene = strtrim(gene, 15))
      
      #####Join with gene annotation
      gwas_file <- left_join(gwas_file, gene_anno, by=c("gene"="gene_id"))
      
      #####Check the join worked
      head(gwas_file)
      nrow(gwas_file)
      
      #####Remove rows with missing data
      gwas_file <- na.omit(gwas_file)
      nrow(gwas_file)  # confirm rows remain
      
      #####Add -log10(pvalue) column
      gwas_file$logP <- as.numeric(-log10(gwas_file$pvalue))
      
      #####Strip the "chr" prefix from the chr column, ensure correct numeric ordering
      gwas_file$chr <- gsub("chr", "", gwas_file$chr)
      gwas_file$chr <- factor(gwas_file$chr, levels = as.character(1:22))
      levels(gwas_file$chr)  # should show "1" "2" "3" ... "22" in order
      head(gwas_file$chr)  # should now show "1", "2", etc. not "chr1", "chr2"
      
      #####Calculate cumulative base pair positions for the x-axis
      gwas_file <- gwas_file %>% group_by(chr) %>% summarise(chr_len=max(start)) %>% 
        mutate(tot=cumsum(as.numeric(chr_len))-chr_len) %>% select(-chr_len) %>% 
        left_join(gwas_file, ., by=c("chr"="chr")) %>% 
        arrange(chr, start) %>% mutate(BPcum=start+tot)
      
      #####Calculate chromosome center positions for x-axis labels
      axisdf <- gwas_file %>% group_by(chr) %>% summarize(center=(max(BPcum) + min(BPcum))/2)
      
      #####Define title and output path
      title <- paste('GCST90274713 TWAS - All Tissues', sep=' ')
      pathTitle <- paste("/home/ohizu/OH1deULTIMATE/ohizu_THESIS/GCST90274713_manhattan.png", sep='')
      
      ##### AND now that you've done all that you can now build the actual plot
      ggplot(gwas_file, aes(x = BPcum, y = logP)) + 
        theme_bw() +
        geom_point(alpha=0.75, size = 2, aes(color = tissue, shape= tissue), show.legend=TRUE) + 
        ggtitle(title) + 
        scale_x_continuous(label = axisdf$chr, breaks = axisdf$center) + 
        scale_color_manual(values = met.brewer("Nizami", 13, type = "continuous")) + 
        scale_shape_manual(values=c(1,2,3,4,5,6,7,8,9,10,11,12,13)) +
        labs(x = "Chromosome", y = "-log10(p)") + 
        geom_hline(yintercept = -log10(5.00e-08), color = "grey40", linetype = "dashed") + 
        theme(axis.text.x = element_text(angle = 60, size = 12, vjust = 0.5), legend.text= element_text(size=6))

      ##### AND THEN, if the plot actually works, you can save now
      ggsave(pathTitle, plot=last_plot(), width = 10, height = 7)
      
####TIME FOR FURTHER ANALYSIS 
      ####PCA
      ######Reshape the data so that rows are genes and columns are tissues — PCA needs data in this wide format
      pca_wide <- Total %>% 
      select(gene, tissue, zscore) %>%
        pivot_wider(names_from = tissue, values_from = zscore)PCA
      
      ######Set gene as the row name and remove it as a column
      pca_matrix <- as.data.frame(pca_wide)
      rownames(pca_matrix) <- pca_matrix$gene
      pca_matrix <- pca_matrix[, -1]  # remove gene column
     
     ######Check the dimensions
       dim(pca_matrix)  # should be genes x tissues
      
    ######Remove rows with missing values
       pca_matrix <- na.omit(pca_matrix)
       nrow(pca_matrix)  # confirm rows remain
    
    ####Run the actual PCA
       
       pca_matrix_t <- t(pca_matrix)
       dim(pca_matrix_t)  # should be tissues x genes
       
    ######Remove gene columns with zero variance   
       pca_matrix_t_filtered <- pca_matrix_t[, apply(pca_matrix_t, 2, var) > 0]
       dim(pca_matrix_t_filtered)  # confirm how many genes remain
       
       
    ######Rerun PCA on the filtered matrix
       pca_result <- prcomp(pca_matrix_t_filtered, center = TRUE, scale. = TRUE)
       summary(pca_result)
       
       
       ###Check variance explained  
       pca_var <- summary(pca_result)$importance
       pca_var[, 1:5]
       
       
       
       
       pca_df <- as.data.frame(pca_result$x)
       pca_df$tissue <- rownames(pca_df)
       head(pca_df)  
       
       
       pc1_var <- round(summary(pca_result)$importance[2,1] * 100, 1)
       pc2_var <- round(summary(pca_result)$importance[2,2] * 100, 1)
       
       
       library(ggrepel)
       
       ggplot(pca_df, aes(x = PC1, y = PC2, label = tissue)) +
         geom_point(aes(color = tissue), size = 4) +
         geom_text_repel(size = 3, 
                         max.overlaps = Inf,
                         box.padding = 0.5,
                         point.padding = 0.3,
                         segment.color = "grey50",
                         segment.size = 0.3) +
         theme_bw() +
         labs(title = "PCA of TWAS Results - GCST90274713",
              x = paste0("PC1 (", pc1_var, "% variance explained)"),
              y = paste0("PC2 (", pc2_var, "% variance explained)")) +
         theme(legend.position = "none",
               plot.title = element_text(size = 12))
   
       
       ggsave("/home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/GCST90274713_screeplot.png",
              plot = last_plot(), width = 8, height = 6)
       
      ####BAR GRAPH
       ######Start by reading in the master file
       Total <- data.table::fread("GCST90274713_AllTissues_Total.csv", header = TRUE, sep = ",")
       
       #####Filter to include only p-values below 5e-8
       Total_filtered <- Total[Total$pvalue < 5e-8, ]
       nrow(Total_filtered)  # check how many rows remain
       
       #####For genes expressed in multiple tissues, keep only the row with the lowest p-value per gene
       Total_dedup <- Total_filtered %>%
         group_by(gene) %>%
         slice_min(order_by = pvalue, n = 1, with_ties = FALSE) %>%
         ungroup()
       nrow(Total_dedup)  # check how many unique genes remain
       
       ####Check again so as to confirm each gene appears only once
       sum(duplicated(Total_dedup$gene))  # should return 0
       
       #####You can count associations per tissue from the new ultra filtered data
       head(Total_dedup[, c("gene", "pvalue", "tissue")])
       table(Total_dedup$tissue)  # see how many top hits came from each tissue
       
 
       tissue_counts_dedup <- Total_dedup %>%
         group_by(tissue) %>%
         summarise(gene_count = n()) %>%
         arrange(-gene_count)
       tissue_counts_dedup
       
       #####AND NOW you can uild the bar graph -- And Save     
       ggplot(tissue_counts_dedup, aes(x = reorder(tissue, -gene_count), y = gene_count)) +
         geom_bar(stat = "identity", fill = "steelblue") +
         theme_bw() +
         labs(title = "Number of Significant Gene Associations per Tissue (p < 5e-8)\nGCST90274713 - Deduplicated",
              x = "Tissue",
              y = "Number of Genes") +
         theme(axis.text.x = element_text(angle = 45, hjust = 1, size = 10),
               axis.text.y = element_text(size = 10),
               plot.title = element_text(size = 12))
       
       ggsave("/home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/GCST90274713_tissue_counts_dedup.png",
              plot = last_plot(), width = 10, height = 7)
       
      ####First you need to sort the master file by p-value, then save the sorted values as a new spreadsheet
      sig_genes <- gwas_file[gwas_file$pvalue < 5.00e-08, ]
      sig_genes <- sig_genes[order(sig_genes$pvalue), ]
      Total <- data.table::fread("GCST90274713_AllTissues_Total.csv", header = TRUE, sep = ",")
      data.table::fwrite(sig_genes, "GCST90274713_sig_genes_sorted.csv", append = FALSE, quote = "auto", sep = ",")
      
      ####Submit the sorted values to FUMA for those analyses and await the results
      
      ####Now you can make the bar graph of associations
      ggplot(tissue_counts, aes(x = reorder(tissue, -gene_count), y = gene_count)) +
        geom_bar(stat = "identity", fill = "steelblue") +
        theme_bw() +
        labs(title = "Number of Significant Genes per Tissue - GCST90274713",
             x = "Tissue",
             y = "Number of Genes") +
        theme(axis.text.x = element_text(angle = 45, hjust = 1, size = 10),
              axis.text.y = element_text(size = 10),
              plot.title = element_text(size = 12))
      
      
####WE WILL TRY LDSC -- WORK IN PROGRESS
      #####First you need to import the LDSC repository from GitHub
      git clone https://github.com/bulik/ldsc.git /home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/ldsc_fresh
      
      #####Then you need to make your own conda environment compatible with python 2.7 -- It also needs to have all the necessary packages
      conda create -p /home/ohizu/OH1deULTIMATE/my_ldsc python=2.7 pandas numpy scipy bitarray
      
      #####Next is to activate the personal python environment and then confirm that pandas is available using the full python path
      conda activate /home/ohizu/OH1deULTIMATE/my_ldsc
      /home/ohizu/OH1deULTIMATE/my_ldsc/bin/python -c "import pandas; print(pandas.__version__)"
      
      ####After that you need to extract the LD reference files and then confirm they're in the right location
      tar -xzvf /home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/eur_w_ld_chr.tar.gz -C /home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/
      ls /home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/eur_w_ld_chr/
        
      ####Munge Sumstats -- To reformat sumstats for LDSC
        /home/ohizu/OH1deULTIMATE/my_ldsc/bin/python /home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/ldsc_fresh/munge_sumstats.py --sumstats /home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/hg38_SPx_GCST90274713.h_sumstats.tsv.gz --snp rsid --a1 effect_allele --a2 non_effect_allele --p pvalue --signed-sumstats effect_size,0 --frq effect_allele_frequency --N-col sample_size --merge-alleles /home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/w_hm3.snplist --out /home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/GCST90274713_munged
      
      #####Run the heritability estimation
      /home/ohizu/OH1deULTIMATE/my_ldsc/bin/python /home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/ldsc_fresh/ldsc.py --h2 /home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/GCST90274713_munged.sumstats.gz --ref-ld-chr /home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/eur_w_ld_chr/ --w-ld-chr /home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/eur_w_ld_chr/ --out /home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/GCST90274713_h2
      cat /home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/GCST90274713_h2.log ###To view the results
      
      ####Make a table of the results
      ldsc_results <- data.frame(
        Metric = c("Total Observed Scale h2", "Standard Error (h2)",
                   "Lambda GC", "Mean Chi^2",
                   "Intercept", "Standard Error (Intercept)",
                   "Ratio", "Standard Error (Ratio)"),
        Value = c(0.0557, 0.0065,
                  1.4387, 2.1479,
                  1.1648, 0.0185,
                  0.1435, 0.0161)
      )
      
      write.csv(ldsc_results,
                "/home/ohizu/OH1deULTIMATE/ohizu_THESIS/TiWASavage/GCST90274713_ldsc_h2_results.csv",
                row.names = FALSE)
      
      

      
