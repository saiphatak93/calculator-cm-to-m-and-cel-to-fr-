# calculator-cm-to-m-and-cel-to-fr-
import 'package:flutter/material.dart';

void main() {
  runApp(const CelsiusConverterApp());
}

class CelsiusConverterApp extends StatelessWidget {
  const CelsiusConverterApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: const ConverterScreen(),
    );
  }
}

class ConverterScreen extends StatefulWidget {
  const ConverterScreen({Key? key}) : super(key: key);

  @override
  _ConverterScreenState createState() => _ConverterScreenState();
}

class _ConverterScreenState extends State<ConverterScreen> {
  final TextEditingController _celsiusController = TextEditingController();
  final TextEditingController _centimeterController = TextEditingController();
  String _fahrenheitResult = '';
  String _meterResult = '';

  // Convert Celsius to Fahrenheit
  void _convertToFahrenheit() {
    String celsiusText = _celsiusController.text;
    if (celsiusText.isNotEmpty) {
      double celsius = double.tryParse(celsiusText) ?? 0;
      double fahrenheit = (celsius * 1.8) + 32;
      setState(() {
        _fahrenheitResult = '${fahrenheit.toStringAsFixed(2)} °F';
      });
    } else {
      setState(() {
        _fahrenheitResult = 'Please enter a value';
      });
    }
  }

  // Convert Centimeters to Meters
  void _convertToMeters() {
    String centimeterText = _centimeterController.text;
    if (centimeterText.isNotEmpty) {
      double centimeters = double.tryParse(centimeterText) ?? 0;
      double meters = centimeters / 100;
      setState(() {
        _meterResult = '${meters.toStringAsFixed(2)} m';
      });
    } else {
      setState(() {
        _meterResult = 'Please enter a value';
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Converter App'),
        backgroundColor: Colors.green,
      ),
      backgroundColor: Colors.greenAccent,
      body: Center(
        child: Padding(
          padding: const EdgeInsets.all(16.0),
          child: Container(
            padding: const EdgeInsets.all(20),
            decoration: BoxDecoration(
              color: Colors.white,
              borderRadius: BorderRadius.circular(15),
              boxShadow: [
                BoxShadow(
                  color: Colors.black26,
                  blurRadius: 5,
                  spreadRadius: 2,
                  offset: Offset(0, 3),
                ),
              ],
            ),
            child: Column(
              mainAxisSize: MainAxisSize.min,
              children: [
                const Text(
                  'Flutter Project by Sai Phatak 106',
                  style: TextStyle(
                    fontSize: 20,
                    fontWeight: FontWeight.bold,
                    color: Colors.green,
                  ),
                ),
                const SizedBox(height: 20),

                // Celsius to Fahrenheit Input & Result
                TextField(
                  controller: _celsiusController,
                  decoration: const InputDecoration(
                    labelText: 'Enter Celsius',
                    border: OutlineInputBorder(),
                  ),
                  keyboardType: TextInputType.number,
                ),
                const SizedBox(height: 10),
                ElevatedButton(
                  onPressed: _convertToFahrenheit,
                  child: const Text('Convert to Fahrenheit'),
                ),
                const SizedBox(height: 10),
                Text(
                  _fahrenheitResult,
                  style: const TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
                ),
                const SizedBox(height: 20),

                // Centimeter to Meter Input & Result
                TextField(
                  controller: _centimeterController,
                  decoration: const InputDecoration(
                    labelText: 'Enter Centimeters',
                    border: OutlineInputBorder(),
                  ),
                  keyboardType: TextInputType.number,
                ),
                const SizedBox(height: 10),
                ElevatedButton(
                  onPressed: _convertToMeters,
                  child: const Text('Convert to Meters'),
                ),
                const SizedBox(height: 10),
                Text(
                  _meterResult,
                  style: const TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
