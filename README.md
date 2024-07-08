Here's a glimpse of the core code for building the buttons and handling input:
import 'package:flutter/material.dart';

void main() {
  runApp(CalculatorApp());
}

class CalculatorApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'AHMED MAAZ',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        brightness: Brightness.dark,
      ),
      home: Calculator(),
    );
  }
}

class Calculator extends StatefulWidget {
  @override
  _CalculatorState createState() => _CalculatorState();
}

class _CalculatorState extends State<Calculator> {
  String _output = "0";
  String _input = "";
  String _operation = "";
  double _num1 = 0.0;
  double _num2 = 0.0;

  void buttonPressed(String buttonText) {
    setState(() {
      if (buttonText == "CLEAR") {
        _output = "0";
        _input = "";
        _num1 = 0.0;
        _num2 = 0.0;
        _operation = "";
      } else if (buttonText == "+" || buttonText == "-" || buttonText == "/" || buttonText == "x") {
        _num1 = double.parse(_output);
        _operation = buttonText;
        _output = "0";
        _input += " $buttonText ";
      } else if (buttonText == ".") {
        if (_output.contains(".")) {
          return;
        } else {
          _output += buttonText;
          _input += buttonText;
        }
      } else if (buttonText == "=") {
        _num2 = double.parse(_output);

        if (_operation == "+") {
          _output = (_num1 + _num2).toString();
        }
        if (_operation == "-") {
          _output = (_num1 - _num2).toString();
        }
        if (_operation == "x") {
          _output = (_num1 * _num2).toString();
        }
        if (_operation == "/") {
          _output = (_num1 / _num2).toString();
        }

        _operation = "";
        _input = _output;
      } else {
        if (_output == "0") {
          _output = buttonText;
        } else {
          _output += buttonText;
        }
        _input += buttonText;
      }
    });
  }

  Widget buildButton(String buttonText, Color color) {
    return Expanded(
      child: Container(
        margin: EdgeInsets.all(5.0),
        child: ElevatedButton(
          style: ElevatedButton.styleFrom(
            padding: EdgeInsets.all(24.0),
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.circular(10.0),
            ),
            primary: color,
          ),
          child: Text(
            buttonText,
            style: TextStyle(
              fontSize: 20.0,
              fontWeight: FontWeight.bold,
              color: Colors.white,
            ),
          ),
          onPressed: () => buttonPressed(buttonText),
        ),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
            'Calculator'),
      ),
      body: SingleChildScrollView(
        child: Column(
          children: <Widget>[
            Container(
              alignment: Alignment.centerRight,
              padding: EdgeInsets.symmetric(
                vertical: 24.0,
                horizontal: 12.0,
              ),
              child: Text(
                _input,
                style: TextStyle(
                  fontSize: 24.0,
                  fontWeight: FontWeight.bold,
                  color: Colors.white,
                ),
              ),
            ),
            Container(
              alignment: Alignment.centerRight,
              padding: EdgeInsets.symmetric(
                vertical: 24.0,
                horizontal: 12.0,
              ),
              child: Text(
                _output,
                style: TextStyle(
                  fontSize: 48.0,
                  fontWeight: FontWeight.bold,
                  color: Colors.white,
                ),
              ),
            ),
            Divider(),
            Column(
              children: [
                Row(
                  children: <Widget>[
                    buildButton("7", Colors.cyanAccent),
                    buildButton("8", Colors.cyanAccent),
                    buildButton("9", Colors.cyanAccent),
                    buildButton("/", Colors.orange)
                  ],
                ),
                Row(
                  children: <Widget>[
                    buildButton("4", Colors.cyanAccent),
                    buildButton("5", Colors.cyanAccent),
                    buildButton("6", Colors.cyanAccent),
                    buildButton("x", Colors.orange)
                  ],
                ),
                Row(
                  children: <Widget>[
                    buildButton("1", Colors.cyanAccent),
                    buildButton("2", Colors.cyanAccent),
                    buildButton("3", Colors.cyanAccent),
                    buildButton("-", Colors.orange)
                  ],
                ),
                Row(
                  children: <Widget>[
                    buildButton(".", Colors.cyanAccent),
                    buildButton("0", Colors.cyanAccent),
                    buildButton("00", Colors.cyanAccent),
                    buildButton("+", Colors.orange)
                  ],
                ),
                Row(
                  children: <Widget>[
                    buildButton("CLEAR", Colors.red),
                    buildButton("=", Colors.green),
                  ],
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }
}
