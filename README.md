
Notebook| Input| Output

--------|------------------------------|---------------------
00_extract_Index_Stimulus_rawData_fromIntanRHD.ipynb (load-rhd-notebook-python-main folder)| 1_RHD_Files- RHD file with raw Intan neural recordings and stimulus data| 3_ReadRHD_Files- RawStimulusData.csv & index.csv
1_Extract_Store_TimeStamps.ipynb| 3_ReadRHD_Files- RawStimulusData.csv & index.csv + 2_Spikesorted_Files- timestamp and units data file exported from Plexon| 4_RawData_Index_Timestamp- timestamps.pickle(unscaled)
1a_convertVoltToDegrees.ipynb| 4_RawData_Index_Timestamp- timestamps.pickle(unscaled)|  4_RawData_Index_Timestamp/ScaledStimulus- timeStamps_scaled.pickle(voltage scaling, not yet angle)
1b_DegreeConversion.ipynb|2b_OtherFilesNeededForAnalysis/motorcalibrationvalues.csv + 4_RawData_Index_Timestamp/ScaledStimulus- timeStamps_scaled.pickle| 4_RawData_Index_Timestamp/ScaledStimulus- _DisplacementIndegrees.csv and _timeStamps_degrees.pickle for angle data with moths where motor attachment distance is known. Also- moth attachmentdistance.csv.
1c_CheckDegreeConversion.ipynb| 4_RawData_Index_Timestamp- timestamps.pickle and angle data dataFolder/4_RawData_Index_Timestamp/ScaledStimulus/*degrees.csv and 4_RawData_Index_Timestamp/ScaledStimulus to visualise  raw voltage, scaled voltage and angle displacement waveforms| Figures/1_Scaled_Stimulus- three plot figure with raw voltage, scaled voltage and angle displacement
2_CreateRaster.ipynb|4_RawData_Index_Timestamp/ScaledStimulus/*_degrees.pickle-for moths with angle data & 4_RawData_Index_Timestamp/ScaledStimulus/*_scaled.pickle for moth remaining in voltage| 4_Raster_PSTH- raster.csv, PSTH.csv, kdefull.csv (all 100 points not just corresponding with PSTH) + Figures/4_Raster_PSTH- combined figure of recording at the top, raster with 30 repeats in centre and PSTH with gaussian kde curve at the bottom
3_Linear-NonLinear_1D.ipynb| 4_RawData_Index_Timestamp/ScaledStimulus/*_degrees.pickle for moths with angle data & 4_RawData_Index_Timestamp/ScaledStimulus/*_scaled.pickle- for moths in voltages| 5_1DCompModel/UnscaledFiringRate_NLD/v2- EncodingModel.pickle- STA/NLD/Prior data
3a_checkNumSpikesInNLDbins.ipynb| 5_1DCompModel/UnscaledFiringRate_NLD/v2/*.pickle- STA/NLD/Prior values| 5_1DCompModel/UnscaledFiringRate_NLD/v2- asCSV file to count check the number of spikes per bin
3aa_SelectUnitBasedOnSTA.ipynb| 5_1DCompModel/UnscaledFiringRate_NLD/v2- EncodingModel.pickle files to analyze which units STA crosses the +-prior mean STD| 5_1DCompModel/selectedUnits.csv- data on which units pass the check
3b_STA_Features_frequencyTuning.ipynb| 5_1DCompModel/Unscaled_clippedNLD/forForwardPrediction/v2/*.pickle, ScaledStimulus pickles| exploratory only — FFT/whitening method development, contains an unresolved bug (cell 5), does not save output
3c_ConditionNLDForPrediction.ipynb| 5_1DCompModel/UnscaledFiringRate_NLD/v2- using the encoding model pickle data + 5_1DCompModel/selectedUnits.csv unit that passed the STA cross check and had filtered out units with too few spikes to make a clipped encoding mode| 5_1DCompModel/Unscaled_clippedNLD/forForwardPrediction/v2/selectedUnits- _EncodingModel.pickle with the units that pass the check data for STA/NLD
3d_Plot_Linear-NonLinear_1D.ipynb| 5_1DCompModel/Unscaled_clippedNLD/forForwardPrediction/v2/selectedUnits/*.pickle- STA/NLD/Prior data for only selected unit| Figures/3_1DCompModel/Unscaled_clippedNLD/FowardPrediction/v2/selectedUnits- plotting the STA/NLD/prior figures for each unit
4_SummaryData.ipynb| 4_RawData_Index_Timestamp/ScaledStimulus+timeStamps_degrees.pickle- to check angle range given by motor for each individual moth & 5_1DCompModel/Unscaled_clippedNLD/forForwardPrediction/v2/selectedUnits- to calculate average of absolute STA peaks from moths with angle data to see range in which they respond + 5b_Latency/selectedUnits/time_to_spike.csv (need to run 4a first- this is summary check) to get mean, median, 75th and 25th percentile| SummaryValuesFinal- STA_anglerangeabs.csv
4a_SummaryData-TimeToSpike.ipynb| 5_1DCompModel/UnscaledFiringRate_NLD/v2+EncodingModel.pickle & 5_1DCompModel/selectedUnits.csv to filter only selected units| 5b_Latency/selectedUnits- values of time of STA crossing (first-crossing latency) & Figures/5b_Latency/selectedUnits- boxplot figure of all the latencies from saved values
4b_SummaryData_LatencyAbsPeak.ipynb| 5_1DCompModel/Unscaled_clippedNLD/forForwardPrediction/v2/selectedUnits/*.pickle- EncodingModel for selected units| 5b_Latency/selectedUnits_peak- csv with values of time of abs peak STA (peak latency, distinct from 4a's first-crossing latency) & Figures/5b_Latency/selectedUnits- boxplot figure of same
4c_SummaryData_NLDCurvature.ipynb| 5_1DCompModel/Unscaled_clippedNLD/forForwardPrediction/v2/selectedUnits+ EncodingModel pickle of selected units to calculate the average NLD slope at the max slope value| Figures/6c_NLDCurvature/selectedUnits- boxplot figure saved & in SummaryValuesFinal- individual unit curvature and mean and median csv files
5_spike_jitter.ipynb| 4_Raster_PSTH + raster.csv to calculate jitter| output in python notebook as check
6_SpikeCheck.ipynb| 1_RHD_Files- load RHD files & 2_Spikesorted_Files & 3_ReadRHD_files+RawStimulusData.csv| Figures/HatCheck- read every spike waveform and average waveform and stimulus around spike window to give figures
7_SelectedUnitsFFT.ipynb| 5_1DCompModel/Unscaled_clippedNLD/forForwardPrediction/v2/selectedUnits- load STA data from encoding model pickle to check frequency magnitude present| Figures/6d_STA_FFT- overlay FFT plot of each unit.
8_SpectralWhitening.ipynb| 5_1DCompModel/UnscaledFiringRate_NLD/v2- EncodingModel.pickle & ScaledStimulus- degree/scaled pickles| Figures/Whitened_STA- whitened STA plot per unit (spectral division whitening method)
8a_WhiteNoiseGeneration-FFT.ipynb| ScaledStimulus- one moth's scaled pickle (hardcoded to m31_wn2)| Figures/6_GeneratedWhiteNoise- generated-vs-recorded stimulus FFT comparison plot; QC check on stimulus generation parameters, not part of main analysis chain

*all input and output for the codes are within the dataFolder.

2_Spikesorted_Files/*.txt (input, from Plexon)
Columns: Timestamp, Unit

2_Spikesorted_Files/ReadMe.txt (input)
Columns: FileID, channelSorted

2b_OtherFilesNeededForAnalysis/motorcalibrationvalues.csv (input)
Columns: parameter, value, units — rows are slope_m and intercept_b

00_extract... output
{moth}_index.csv: index_starts, index_stops
{moth}_RawStimulusData.csv: stimulus
{moth}_rawNeuralData.csv: raw_neural_trace (not used downstream)

1_Extract_Store_TimeStamps output — {moth}_timeStamps.pickle (3-element tuple)
[0] all_Units_aligned — dict: unit_0, unit_1... → list of arrays (spike times in sec, one array per repeat)
[1] all_Units_prior — dict: same keys → list (per repeat) of lists of random prior timepoints
[2] WhiteNoise — raw ADC voltage stimulus, pd.Series indexed in seconds

1a output
{moth}_timeStamps_scaled.pickle: same 3-tuple, index [2] now scaled ±5V, mean-centered
scaling_info.csv: parameter, value, units

1b output
{moth}_timeStamps_degrees.pickle: same 3-tuple, index [2] now in degrees
{moth}_DisplacementIndegrees.csv: raw_voltage, scaled_voltage, displacement_cm, deflectionAngle_degrees
moth_attachment_distances.csv: moth, attachment_distance_cm

1c output: no csv/pickle — PNG figures only

2_CreateRaster output
{moth}_{unit}_raster.csv: repeat, spike_time
{moth}_{unit}_psth.csv: bin_center, firing_rate, kde_at_bin
{moth}_{unit}_kde_full.csv: time, kde

3_Linear-NonLinear_1D output — {moth}_{unit}_EncodingModel.pickle (12-element tuple, indices 0–11)
[0] ste — spike-triggered ensemble (all pre-spike snippets)
[1] sta — spike-triggered average
[2] sta_error — SD of ste
[3] prior_ensemble — snippets at random prior timepoints
[4] prior_mean
[5] prior_error — SD of prior ensemble
[6] prior_std — scalar, projected prior SD (z-score normalizer)
[7] mean_fire_rate — scalar
[8] nld — firing probability per bin
[9] n_ste — spike counts per bin
[10] n_prior — prior counts per bin
[11] bin_centers

3a output
{moth}_{unit}_asCSV.csv: count_ste, count_prior, count_nld, bin_centers

3aa output
selectedUnits.csv: mothID, up (crossing index, if upward), down (crossing index, if downward), status (non-null = passed)

3b output: none — exploratory/method-development notebook only, does not save any file

3c output — same pickle as step 3, plus indices 12–13
[12] bin_fwdModel — clipped bin centers (n_ste≥50, ±2.5 z-score)
[13] nld_fwdModel — clipped NLD values

3d output: no csv/pickle — PDF figures only

4_SummaryData output
SummaryValuesFinal/STA_anglerangeabs.csv: mothID, sta_max_amplitude, group (degrees/volts)

4a_SummaryData-TimeToSpike output (first-crossing latency — when STA first exits prior mean ± error band)
5b_Latency/selectedUnits/time_to_spike.csv: mothID, time_up, time_down, merged
SummaryValuesFinal/timetospike_summary.csv: mothID, time_up, time_down, merged, latency_ms

4b_SummaryData_LatencyAbsPeak output (peak latency — time of STA's single max |deflection|, no prior comparison; distinct metric from 4a)
5b_Latency/selectedUnits_peak/absolute_peak.csv: moth, unit, latency_ms, peak_value, peak_sign
Figures/5b_Latency/selectedUnits/STA_peak_latency_boxplot.pdf, .png: peak latency boxplot (note: figure saved to a different folder — selectedUnits, not selectedUnits_peak — than the csv above)

4c_SummaryData_NLDCurvature output
SummaryValuesFinal/nld_curvature_summary.csv: mothID, av_max, av_max_bin, local_max, local_max_bin_pre, local_max_bin_post
SummaryValuesFinal/nld_curvature_summary_stats.csv: metric, value

5_spike_jitter, 6_SpikeCheck, 7_SelectedUnitsFFT, 8_SpectralWhitening, 8a_WhiteNoiseGeneration-FFT: no csv/pickle output — figures only (as noted in the pipeline table above)
