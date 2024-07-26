from Bio import SeqIO

fastq_file = "file path"

protein_sequences = []

concatenated_protein_sequence_parts = []

search_sequences = ["TQMNLKYAISAKNRARTVAGVSI", "PHLMGWDYPKCDRAMPNM", "RFYRLANECAQVLSE", "YVKPGGTSSGDATTAYANSVFNI", "LYYQNNVFMSEAKCW", "AGCFVDDIVKTDGTLM", "ERFVSLAIDAYPLTKH", "CIRRPFLCCKCCYDHVI", "QGPPGTGKSHFAIGLA", "VYTACSHAAVDALCEKA", "NLPGCDGGSLYVNKHAFHTPA", "KCTSVVLLSVLQQL", "VRKIFVDGVPFVVS", "LKHFFFAQDGNAAI", "GDPAQLPAPRTLLT", "KAVFISPYNSQNAV", "NMRVIHFGAGSDK"] 

record_count = 0
for record in SeqIO.parse(fastq_file, "fastq"):
    record_count += 1
    if record_count % 1000 == 0:
        print(f"Processed {record_count} records")

    dna_sequence = record.seq

    dna_sequence = dna_sequence.replace('N', 'A')

    protein_sequence = dna_sequence.translate(to_stop=True)

    concatenated_protein_sequence_parts.append(str(protein_sequence))

concatenated_protein_sequence = ''.join(concatenated_protein_sequence_parts)

found_sequences_count = 0
for search_sequence in search_sequences:
    if search_sequence in concatenated_protein_sequence:
        found_sequences_count += 1

if found_sequences_count >= 1:
    print("Betacoronavirus detected.")
else:
    print("Betacoronavirus not detected.")
