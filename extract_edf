import pylink
import matplotlib.pyplot as plt
import numpy as np

# Connect to the Eyelink tracker
eyelink = pylink.EyeLink()

# Load the EDF file
edf_file = "my_experiment.edf"
eyelink.openDataFile(edf_file)

# Extract the gaze data
sample_rate = eyelink.getTrackerSampleRate()
gaze_data = eyelink.getNewestSample().getGaze()

# Set up the plot
fig, ax = plt.subplots()
ax.set_xlim(0, 1280)
ax.set_ylim(0, 1024)
line, = ax.plot([], [], 'o-', lw=2)

# Define the size of the gaze window
window_size = 100

# Initialize the gaze history array
gaze_history = np.zeros((window_size, 2))

# Continuously update the gaze window and plot the gaze data
while True:
    # Get the latest gaze data
    gaze_data = eyelink.getNewestSample().getGaze()
    x, y = gaze_data[-2:]

    # Add the latest gaze position to the gaze history
    gaze_history[:-1] = gaze_history[1:]
    gaze_history[-1] = [x, y]

    # Update the plot with the new gaze history
    line.set_data(gaze_history[:, 0], gaze_history[:, 1])
    plt.pause(0.01)

# Close the EDF file and disconnect from the Eyelink tracker
eyelink.closeDataFile()
eyelink.close()
