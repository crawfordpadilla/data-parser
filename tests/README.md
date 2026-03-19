# data_parser.py
import json
import logging

# Set up logging
logging.basicConfig(level=logging.INFO)

class DataParser:
    def __init__(self, file_path):
        """Initialize the DataParser with a file path."""
        self.file_path = file_path

    def parse(self):
        """Parse the data from the file and return it as a dictionary."""
        try:
            with open(self.file_path, 'r') as file:
                data = json.load(file)
                logging.info("Parsed data: %s", data)
                return data
        except FileNotFoundError:
            logging.error("File not found: %s", self.file_path)
            return None
        except json.JSONDecodeError as e:
            logging.error("Failed to parse JSON: %s", e)
            return None

def main():
    parser = DataParser('data.json')
    data = parser.parse()
    if data:
        print(data)

if __name__ == "__main__":
    main()