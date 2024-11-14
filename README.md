# Pipeline Leak Detection System using AI and Machine Learning

## Overview
This project presents an intelligent system for detecting fluid leaks in industrial pipelines using a combination of hardware components and machine learning. The system uses the Seeed Wio Terminal, a DFRobot Water Flow sensor, and a custom-trained AI model to monitor liquid flow and identify potential leaks in real-time. By analyzing flow rate data, the AI model classifies the state of the pipeline into three categories: no flow, normal flow, and leak. This approach helps protect the environment, reduce health risks, and prevent costly damage to pipelines.
![pic1](https://github.com/user-attachments/assets/12c145f7-b4b6-406a-b47c-741df297c8d6)

## Hardware Setup
### Components:
- **Seeed Wio Terminal**: A development board with a built-in screen, input/output interfaces, and an enclosure.
- **DFRobot Water Flow Sensor**: Detects the flow of liquid by using a magnetic rotor and Hall Effect sensor, which outputs a pulse-width signal based on the liquid flow rate.
- **Pipes**: Used to connect the sensor to the pipeline to measure flow, no flow, and leak conditions.

### Wiring:
- Connect the **Water Flow Sensor** to the Wio Terminal for data acquisition.
- The sensor outputs a PWM signal which is used to calculate the flow rate.

## Software Setup
### Data Collection:
1. Upload the **DataCollection.ino** sketch to the Wio Terminal.
2. Connect the Wio Terminal to your computer.
3. Run the **SerialDataCollection.py** script on your computer to start collecting data.
4. Press **Button C** on the Wio Terminal to begin recording.
5. Press **Button C** again to stop recording when enough data has been collected.
6. The data is saved as a CSV file. Label the file according to the flow state (e.g., no flow, normal flow, leak).
7. Upload the CSV files to **Edge Impulse** using the Data Acquisition tab.

### Impulse Design:
1. Use **Time Series Data** as the input block for the model.
2. Set the **Raw Data** as the processing block for feature extraction.
3. Select **Classification** as the learning block to categorize the flow into three classes (no flow, normal flow, and leak).
4. Split the dataset into training and testing sets.
5. Generate features and ensure the data is well-separated.

### Model Training:
1. Train the model using **Edge Impulse** with the provided dataset.
2. Adjust the model's parameters to achieve satisfactory training accuracy (100% in this case).
3. Test the model with unseen data to ensure 100% testing accuracy.

### Deployment:
1. Once the model is trained, build an **Arduino Library** from the Deployment tab in **Edge Impulse**.
2. Add the library to the **Arduino IDE** via **Sketch > Include Library > Add .ZIP library**.
3. Modify the **static_buffer.ino** file located in **File > Examples > Your Project Name > static_buffer > static_buffer.ino** for dynamic inference.

## Final Output
After deploying the model, the system will detect the flow status of the pipeline and classify it into three states:
- **No Flow**: No liquid is flowing through the sensor.
- **Normal Flow**: Liquid is flowing as expected.
- **Leak**: A leakage is detected, indicating a potential issue in the pipeline.

## Results
- The AI model achieved 100% accuracy during both training and testing, making it highly reliable for detecting leaks in real-world scenarios.
- The system can be deployed for continuous monitoring of pipelines, offering an early warning for potential issues.

## Future Improvements
- Incorporate additional sensors for more comprehensive monitoring (e.g., pressure sensors).
- Implement real-time notifications for detected leaks.
- Enhance the model with more data to improve accuracy in different environmental conditions.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
