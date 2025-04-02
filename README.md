import numpy as np
import matplotlib.pyplot as plt

def analyze_transformer_oil(breakdown_voltage, moisture_content, acidity, dga_h2, dga_co):
    """
    Function to analyze transformer oil condition based on input parameters.
    
    Parameters:
    breakdown_voltage (float): Breakdown voltage in kV.
    moisture_content (float): Moisture content in ppm.
    acidity (float): Acidity in mgKOH/g.
    dga_h2 (float): Dissolved hydrogen levels in ppm.
    dga_co (float): Dissolved carbon monoxide levels in ppm.
    
    Returns:
    dict: Analysis results indicating the condition of the transformer oil.
    """
    # Threshold values (example values, adjust based on real data)
    breakdown_voltage_threshold = 30  # in kV
    moisture_content_threshold = 35  # in ppm
    acidity_threshold = 0.3  # in mgKOH/g
    dga_h2_threshold = 150  # in ppm
    dga_co_threshold = 500  # in ppm
    
    results = {}
    
    # Breakdown Voltage Analysis
    results['Breakdown Voltage'] = "Good" if breakdown_voltage > breakdown_voltage_threshold else "Bad"
    
    # Moisture Content Analysis
    results['Moisture Content'] = "Safe" if moisture_content < moisture_content_threshold else "High Moisture Risk"
    
    # Acidity Analysis
    results['Acidity'] = "Normal" if acidity < acidity_threshold else "High Acidity - Requires Action"
    
    # Dissolved Gas Analysis (DGA)
    results['Hydrogen Levels'] = "Safe" if dga_h2 < dga_h2_threshold else "Warning: Potential Fault"
    results['Carbon Monoxide Levels'] = "Safe" if dga_co < dga_co_threshold else "Warning: Insulation Degradation"
    
    return results

def get_user_inputs():
    """Function to get user inputs with error handling."""
    while True:
        try:
            breakdown_voltage = float(input("Enter Breakdown Voltage (kV): "))
            moisture_content = float(input("Enter Moisture Content (ppm): "))
            acidity = float(input("Enter Acidity (mgKOH/g): "))
            dga_h2 = float(input("Enter Dissolved Hydrogen (ppm): "))
            dga_co = float(input("Enter Dissolved CO (ppm): "))
            return breakdown_voltage, moisture_content, acidity, dga_h2, dga_co
        except ValueError:
            print("Invalid input. Please enter numeric values.")

def visualize_results(analysis_results):
    """Function to visualize the analysis results."""
    labels = list(analysis_results.keys())
    values = [1 if status == "Safe" or status == "Good" or status == "Normal" else 0 for status in analysis_results.values()]
    plt.figure(figsize=(8, 5))
    plt.bar(labels, values, color=['green' if v == 1 else 'red' for v in values])
    plt.xlabel("Parameters")
    plt.ylabel("Status (1 = Good, 0 = Bad)")
    plt.title("Transformer Oil Condition Monitoring")
    plt.xticks(rotation=45)
    plt.show()

# Main execution
if __name__ == "__main__":
    # Get user inputs
    breakdown_voltage, moisture_content, acidity, dga_h2, dga_co = get_user_inputs()
    
    # Analyze the oil condition
    analysis_results = analyze_transformer_oil(breakdown_voltage, moisture_content, acidity, dga_h2, dga_co)

    # Display results
    print("\nTransformer Oil Condition Analysis:")
    for parameter, status in analysis_results.items():
        print(f"{parameter}: {status}")

    # Visualize results
    visualize_results(analysis_results)
# Transformer-Oil-Monitoring-And-Conditionig
