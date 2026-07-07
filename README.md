def calculate_protein_properties(sequence):
    #these are all the avg molecular weights of the amino acids (in Daltons)
    avg_molecular_weights = {
        'A': 89.09, 'R': 174.20, 'N': 132.12, 'D': 133.10, 'C': 121.16,
        'Q': 146.15, 'E': 147.13, 'G': 75.07, 'H': 155.16, 'I': 131.18,
        'L': 131.18, 'K': 146.19, 'M': 149.21, 'F': 165.19, 'P': 115.13,
        'S': 105.09, 'T': 119.12, 'W': 204.23, 'Y': 181.19, 'V': 117.15
    }

    total_mass = 0
    valid_sequence = True

    # Hand empty string inputs
    if len(sequence) == 0:
        print("The input sequence is empty.")
        return None

    for amino_acid in sequence:
        if amino_acid in avg_molecular_weights:
            total_mass += avg_molecular_weights[amino_acid]
        else:
            print(f"Invalid amino acid code: {amino_acid}")
            valid_sequence = False
            break
    if valid_sequence:
    # For bio stuff: subtracting water mass needed for (N-1) peptide bonds
        water_mass = 18.015
        peptide_bonds = len(sequence) - 1
        total_mass = total_mass - (peptide_bonds * water_mass)

        return total_mass
    
    return None

# Get input from user, format to uppercase 
user_input = input("Enter a protein sequence (using single-letter amino acid codes): ").upper()

# Call the function and store returned result
mass = calculate_protein_properties(user_input)

# display output
if mass is not None:
    print(f"The total molecular weight of the protein sequence is: {mass:.2f} Daltons.")
