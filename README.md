- 👋 Hi, I’m @soudpaz
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
soudpaz/soudpaz is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import numpy as np

class Data:
    def __init__(self, data_ptr, num_rows, num_cols):
        self.data_ptr = data_ptr
        self.num_rows = num_rows
        self.num_cols = num_cols
        self.disallowed_split_variables = set()
        self.outcome_index = None
        self.treatment_index = None
        self.instrument_index = None
        self.weight_index = None
        self.causal_survival_numerator_index = None
        self.causal_survival_denominator_index = None
        self.censor_index = None

    def set_outcome_index(self, index):
        self.outcome_index = index

    def set_outcome_index(self, index):
        self.outcome_index = index

    def set_treatment_index(self, index):
        self.treatment_index = index

    def set_treatment_index(self, index):
        self.treatment_index = index

    def set_instrument_index(self, index):
        self.instrument_index = index

    def set_weight_index(self, index):
        self.weight_index = index

    def set_causal_survival_numerator_index(self, index):
        self.causal_survival_numerator_index = index

    def set_causal_survival_denominator_index(self, index):
        self.causal_survival_denominator_index = index

    def set_censor_index(self, index):
        self.censor_index = index

    def get_all_values(self, var):
        samples = list(range(self.num_rows))
        all_values = list(set(self.data_ptr[samples, var]))
        all_values.sort()
        sorted_samples = np.argsort(self.data_ptr[samples, var])
        return sorted_samples

    def get_num_cols(self):
        return self.num_cols

    def get_num_rows(self):
        return self.num_rows

    def get_num_outcomes(self):
        return len(self.outcome_index)

    def get_num_treatments(self):
        return len(self.treatment_index)

    def get_disallowed_split_variables(self):
        return self.disallowed_split_variables

    def get_outcome(self, row):
        return self.get(row, self.outcome_index[0])

    def get_outcomes(self, row):
        return [self.get(row, i) for i in self.outcome_index]

    def get_treatment(self, row):
        return self.get(row, self.treatment_index[0])

    def get_treatments(self, row):
        return [self.get(row, i) for i in self.treatment_index]

    def get_instrument(self, row):
        return self.get(row, self.instrument_index)

    def get_weight(self, row):
        if self.weight_index is not None:
            return self.get(row, self.weight_index)
        else:
            return 1.0

    def get_causal_survival_numerator(self, row):
        return self.get(row, self.causal_survival_numerator_index)

    def get_causal_survival_denominator(self, row):
        return self.get(row, self.causal_survival_denominator_index)

    def is_failure(self, row):
        return self.get(row, self.censor_index) > 0.0

    def get(self, row, col):
        return self.data_ptr[col * self.num_rows + row]

# Example usage:
data_ptr = np.array([...])  # Replace with your actual data array
num_rows = 10  # Replace with your actual number of rows
num_cols = 20  # Replace with your actual number of columns
data = Data(data_ptr, num_rows, num_cols)
data.set_outcome_index([0, 1])  # Replace with your desired outcome indices
data.set_treatment_index([2, 3])  # Replace with your desired treatment indices

# Now you can use the Data class methods to access your data
