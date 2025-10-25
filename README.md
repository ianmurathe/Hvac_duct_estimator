// Flutter code for HVAC Duct Estimator (Wireframe Version)
import 'package:flutter/material.dart';

void main() => runApp(HvacDuctProApp());

class HvacDuctProApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'HVAC DuctPro',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: HomeScreen(),
      routes: {
        '/estimator': (context) => EstimatorScreen(),
        '/results': (context) => ResultsScreen(),
        '/settings': (context) => SettingsScreen(),
      },
    );
  }
}

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('HVAC DuctPro')),
      body: Padding(
        padding: const EdgeInsets.all(20.0),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ElevatedButton(
              onPressed: () => Navigator.pushNamed(context, '/estimator'),
              child: Text('GI Duct Estimator'),
            ),
            ElevatedButton(
              onPressed: () => Navigator.pushNamed(context, '/estimator'),
              child: Text('PAL Duct Estimator'),
            ),
            ElevatedButton(
              onPressed: () {},
              child: Text('Saved Projects'),
            ),
            ElevatedButton(
              onPressed: () => Navigator.pushNamed(context, '/settings'),
              child: Text('Settings'),
            ),
          ],
        ),
      ),
    );
  }
}

class EstimatorScreen extends StatefulWidget {
  @override
  _EstimatorScreenState createState() => _EstimatorScreenState();
}

class _EstimatorScreenState extends State<EstimatorScreen> {
  final lengthController = TextEditingController();
  final widthController = TextEditingController();
  final heightController = TextEditingController();
  final velocityController = TextEditingController(text: '5');
  final rateController = TextEditingController(text: '1500');
  String materialType = 'GI';
  bool insulation = false;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Duct Estimator')),
      body: SingleChildScrollView(
        padding: EdgeInsets.all(16),
        child: Column(
          children: [
            TextField(controller: lengthController, keyboardType: TextInputType.number, decoration: InputDecoration(labelText: 'Length (mm)')),
            TextField(controller: widthController, keyboardType: TextInputType.number, decoration: InputDecoration(labelText: 'Width (mm)')),
            TextField(controller: heightController, keyboardType: TextInputType.number, decoration: InputDecoration(labelText: 'Height (mm)')),
            TextField(controller: velocityController, keyboardType: TextInputType.number, decoration: InputDecoration(labelText: 'Velocity (m/s)')),
            TextField(controller: rateController, keyboardType: TextInputType.number, decoration: InputDecoration(labelText: 'Material Rate (KES/m²)')),
            DropdownButton<String>(
              value: materialType,
              items: ['GI', 'PAL', 'Spiral'].map((e) => DropdownMenuItem(value: e, child: Text(e))).toList(),
              onChanged: (val) => setState(() => materialType = val!),
            ),
            CheckboxListTile(
              title: Text('Insulation Required?'),
              value: insulation,
              onChanged: (val) => setState(() => insulation = val!),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () => Navigator.pushNamed(context, '/results'),
              child: Text('Calculate'),
            ),
          ],
        ),
      ),
    );
  }
}

class ResultsScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Results')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text('Area: -- m²'),
            Text('Hydraulic Diameter: -- m'),
            Text('Airflow: -- m³/s'),
            Text('Friction Loss: -- Pa'),
            Text('Material Cost: -- KES'),
            SizedBox(height: 20),
            ElevatedButton(onPressed: () {}, child: Text('Save Project')),
            ElevatedButton(onPressed: () {}, child: Text('Export PDF')),
            ElevatedButton(onPressed: () => Navigator.pop(context), child: Text('Back')),
          ],
        ),
      ),
    );
  }
}

class SettingsScreen extends StatelessWidget {
  final velocityController = TextEditingController(text: '5');
  final rateController = TextEditingController(text: '1500');

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Settings')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            TextField(controller: velocityController, keyboardType: TextInputType.number, decoration: InputDecoration(labelText: 'Default Velocity (m/s)')),
            TextField(controller: rateController, keyboardType: TextInputType.number, decoration: InputDecoration(labelText: 'Default Material Rate (KES/m²)')),
            SwitchListTile(title: Text('Use Imperial Units'), value: false, onChanged: (val) {}),
          ],
        ),
      ),
    );
  }
}
