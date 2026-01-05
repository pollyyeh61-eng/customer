import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';
import 'dart:convert';
import 'package:intl/intl.dart';
import 'package:url_launcher/url_launcher.dart';

// 網頁版專用：使用最新 package:web 避開舊版 dart:html 的刪除線與編譯錯誤
import 'package:web/web.dart' as web;
import 'dart:js_interop'; 

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  runApp(const CustomerWebPage());
}

class CustomerWebPage extends StatelessWidget {
  const CustomerWebPage({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: '客戶管理系統 - Web版',
      theme: ThemeData(
        primaryColor: const Color(0xFFD4AF37),
        appBarTheme: const AppBarTheme(
          backgroundColor: Color(0xFFD4AF37),
          elevation: 2,
          centerTitle: true,
          titleTextStyle: TextStyle(fontSize: 22, fontWeight: FontWeight.bold, color: Colors.white),
        ),
      ),
      home: const CustomerFormPage(),
    );
  }
}

// --- 客戶資料模型 ---
class Customer {
  String name, phone, bloodType, constellation, nextDate, nextItem, note;
  List<String> historyLogs;

  Customer({
    required this.name,
    this.phone = '', this.bloodType = '',
    this.constellation = '', this.nextDate = '', this.nextItem = '',
    this.note = '', List<String>? historyLogs,
  }) : historyLogs = historyLogs ?? [];

  Map<String, dynamic> toJson() => {
    'name': name, 'phone': phone, 'bloodType': bloodType,
    'constellation': constellation, 'nextDate': nextDate, 'nextItem': nextItem,
    'note': note, 'historyLogs': historyLogs,
  };

  factory Customer.fromJson(Map<String, dynamic> json) => Customer(
    name: json['name'],
    phone: json['phone'] ?? '',
    bloodType: json['bloodType'] ?? '',
    constellation: json['constellation'] ?? '',
    nextDate: json['nextDate'] ?? '',
    nextItem: json['nextItem'] ?? '',
    note: json['note'] ?? '',
    historyLogs: List<String>.from(json['historyLogs'] ?? []),
  );
}

class CustomerFormPage extends StatefulWidget {
  const CustomerFormPage({super.key});
  @override
  State<CustomerFormPage> createState() => _CustomerFormPageState();
}

class _CustomerFormPageState extends State<CustomerFormPage> {
  final Color goldColor = const Color(0xFFD4AF37);
  final _nameController = TextEditingController();
  final _phoneController = TextEditingController();
  final _noteController = TextEditingController();
  final _currentServiceController = TextEditingController();
  final _nextDateController = TextEditingController();
  final _nextItemController = TextEditingController();

  String? _selectedBlood;
  String? _selectedZodiac;
  final List<String> _bloodTypes = ['A', 'B', 'O', 'AB'];
  final List<String> _zodiacs = ['牡羊座', '金牛座', '雙子座', '巨蟹座', '獅子座', '處女座', '天秤座', '天蠍座', '射手座', '摩羯座', '水瓶座', '雙魚座'];

  void _openGoogleCalendar(Customer customer) async {
    if (customer.nextDate.isEmpty) return;
    final String title = Uri.encodeComponent('預約：${customer.name}');
    final String desc = Uri.encodeComponent('項目：${customer.nextItem}\n備註：${customer.note}');
    final String dateFormatted = customer.nextDate.replaceAll(RegExp(r'[- : ]'), '');
    final String url = "https://www.google.com/calendar/render?action=TEMPLATE&text=$title&details=$desc&dates=${dateFormatted}00/${dateFormatted}00";
    
    final uri = Uri.parse(url);
    if (await canLaunchUrl(uri)) {
      await launchUrl(uri);
    }
  }

  Future<void> _saveData() async {
    String name = _nameController.text.trim();
    if (name.isEmpty) {
      ScaffoldMessenger.of(context).showSnackBar(const SnackBar(content: Text('❌ 姓名為必填'), backgroundColor: Colors.red));
      return;
    }
    
    final prefs = await SharedPreferences.getInstance();
    List<String> saved = prefs.getStringList('all_customers') ?? [];
    List<Customer> allList = saved.map((s) => Customer.fromJson(jsonDecode(s))).toList();
    
    String today = DateFormat('yyyy-MM-dd').format(DateTime.now());
    String serviceLog = _currentServiceController.text.trim();
    String newLog = "$today: ${serviceLog.isEmpty ? '無紀錄' : serviceLog}";
    
    late Customer currentCustomer;
    int index = allList.indexWhere((c) => c.name == name);
    
    setState(() {
      if (index != -1) {
        allList[index].historyLogs.insert(0, newLog);
        allList[index].nextDate = _nextDateController.text;
        allList[index].nextItem = _nextItemController.text;
        allList[index].bloodType = _selectedBlood ?? allList[index].bloodType;
        allList[index].constellation = _selectedZodiac ?? allList[index].constellation;
        allList[index].note = _noteController.text;
        allList[index].phone = _phoneController.text;
        currentCustomer = allList[index];
      } else {
        currentCustomer = Customer(
          name: name, phone: _phoneController.text,
          bloodType: _selectedBlood ?? '', constellation: _selectedZodiac ?? '',
          nextDate: _nextDateController.text, nextItem: _nextItemController.text,
          note: _noteController.text, historyLogs: [newLog],
        );
        allList.add(currentCustomer);
      }
    });
    
    await prefs.setStringList('all_customers', allList.map((c) => jsonEncode(c.toJson())).toList());
    
    if (_nextDateController.text.isNotEmpty) _openGoogleCalendar(currentCustomer);
    
    _clear();
    ScaffoldMessenger.of(context).showSnackBar(const SnackBar(content: Text('✅ 資料已安全儲存'), backgroundColor: Colors.green));
  }

  void _clear() {
    _nameController.clear(); _phoneController.clear(); 
    _noteController.clear(); _currentServiceController.clear();
    _nextDateController.clear(); _nextItemController.clear();
    setState(() { _selectedBlood = null; _selectedZodiac = null; });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('客戶管理系統 (Web)'),
        actions: [
          ElevatedButton.icon(
            icon: const Icon(Icons.list, color: Colors.white),
            label: const Text('名單總覽', style: TextStyle(color: Colors.white)),
            onPressed: () => Navigator.push(context, MaterialPageRoute(builder: (context) => const CustomerListPage())),
            style: ElevatedButton.styleFrom(backgroundColor: Colors.white.withOpacity(0.2)),
          ),
          const SizedBox(width: 20),
        ],
      ),
      body: Center(
        child: Container(
          constraints: const BoxConstraints(maxWidth: 800),
          padding: const EdgeInsets.symmetric(vertical: 20, horizontal: 15),
          child: SingleChildScrollView(
            child: Card(
              elevation: 5,
              shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(15)),
              child: Padding(
                padding: const EdgeInsets.all(30),
                child: Column(
                  children: [
                    _buildField(_nameController, '客戶姓名 *', icon: Icons.person),
                    _buildField(_phoneController, '連絡電話', keyboardType: TextInputType.phone, icon: Icons.phone),
                    Row(children: [
                      Expanded(child: _buildDropdown('血型', _bloodTypes, _selectedBlood, (v) => setState(() => _selectedBlood = v))),
                      const SizedBox(width: 15),
                      Expanded(child: _buildDropdown('星座', _zodiacs, _selectedZodiac, (v) => setState(() => _selectedZodiac = v))),
                    ]),
                    const SizedBox(height: 15),
                    _buildField(_noteController, '特別備註 (膚質、喜好等)', maxLines: 2),
                    _buildField(_currentServiceController, '本次服務紀錄內容', maxLines: 2),
                    _buildAppointmentSection(),
                    const SizedBox(height: 30),
                    ElevatedButton(
                      onPressed: _saveData,
                      style: ElevatedButton.styleFrom(
                        backgroundColor: goldColor,
                        minimumSize: const Size(double.infinity, 60),
                        shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(10))
                      ),
                      child: const Text('確認儲存並同步日曆', style: TextStyle(color: Colors.white, fontSize: 18, fontWeight: FontWeight.bold)),
                    ),
                  ],
                ),
              ),
            ),
          ),
        ),
      ),
    );
  }

  Widget _buildAppointmentSection() {
    return Container(
      padding: const EdgeInsets.all(15),
      decoration: BoxDecoration(color: Colors.blueGrey[50], borderRadius: BorderRadius.circular(10), border: Border.all(color: Colors.blueGrey.shade100)),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          const Text("📅 下次預約提醒", style: TextStyle(fontWeight: FontWeight.bold, color: Colors.blueGrey)),
          const SizedBox(height: 10),
          _buildField(_nextItemController, '下次預約項目', bottomPadding: 10),
          TextField(
            controller: _nextDateController, readOnly: true,
            decoration: const InputDecoration(labelText: '日期與時間', suffixIcon: Icon(Icons.calendar_month), border: OutlineInputBorder()),
            onTap: () async {
              DateTime? d = await showDatePicker(context: context, initialDate: DateTime.now(), firstDate: DateTime.now(), lastDate: DateTime(2100));
              if (d != null) {
                TimeOfDay? t = await showTimePicker(context: context, initialTime: TimeOfDay.now());
                if (t != null) {
                  final full = DateTime(d.year, d.month, d.day, t.hour, t.minute);
                  setState(() => _nextDateController.text = DateFormat('yyyy-MM-dd HH:mm').format(full));
                }
              }
            },
          ),
        ],
      ),
    );
  }

  Widget _buildField(TextEditingController c, String l, {int maxLines = 1, TextInputType keyboardType = TextInputType.text, double bottomPadding = 15, IconData? icon}) => 
    Padding(padding: EdgeInsets.only(bottom: bottomPadding), child: TextField(controller: c, maxLines: maxLines, keyboardType: keyboardType, decoration: InputDecoration(prefixIcon: icon != null ? Icon(icon) : null, labelText: l, border: const OutlineInputBorder())));

  Widget _buildDropdown(String label, List<String> items, String? current, ValueChanged<String?> onChanged) =>
    DropdownButtonFormField<String>(decoration: InputDecoration(labelText: label, border: const OutlineInputBorder()), value: current, items: items.map((s) => DropdownMenuItem(value: s, child: Text(s))).toList(), onChanged: onChanged);
}

// --- 客戶列表頁面 ---
class CustomerListPage extends StatefulWidget {
  const CustomerListPage({super.key});
  @override
  State<CustomerListPage> createState() => _CustomerListPageState();
}

class _CustomerListPageState extends State<CustomerListPage> {
  List<Customer> list = [];
  @override
  void initState() { super.initState(); _load(); }
  
  void _load() async {
    final prefs = await SharedPreferences.getInstance();
    List<String> saved = prefs.getStringList('all_customers') ?? [];
    setState(() => list = saved.map((s) => Customer.fromJson(jsonDecode(s))).toList());
  }

  // --- 修正後的網頁下載功能 ---
  void _downloadBackup() {
    if (list.isEmpty) return;
    String content = "客戶資料完整備份\n匯出時間: ${DateFormat('yyyy-MM-dd HH:mm').format(DateTime.now())}\n" + "="*40 + "\n";
    for (var c in list) {
      content += "\n【${c.name}】\n電話：${c.phone}\n血型：${c.bloodType} | 星座：${c.constellation}\n備註：${c.note}\n歷史服務：\n${c.historyLogs.join('\n')}\n" + "-"*30 + "\n";
    }

    // 使用最新 package:web 語法進行下載
    final bytes = utf8.encode(content);
    final blob = web.Blob([bytes.toJS].toJS, web.BlobPropertyBag(type: 'text/plain'));
    final url = web.URL.createObjectURL(blob);
    
    final anchor = web.document.createElement('a') as web.HTMLAnchorElement;
    anchor.href = url;
    anchor.download = "customer_data_backup.txt";
    anchor.click();
    
    web.URL.revokeObjectURL(url);
  }

  void _editCustomer(Customer oldData) {
    final ePhone = TextEditingController(text: oldData.phone);
    final eNote = TextEditingController(text: oldData.note);
    final eHistory = TextEditingController(text: oldData.historyLogs.join('\n'));

    showDialog(
      context: context,
      builder: (ctx) => AlertDialog(
        title: Text('編輯客戶：${oldData.name}'),
        content: SizedBox(
          width: 500,
          child: SingleChildScrollView(
            child: Column(
              mainAxisSize: MainAxisSize.min,
              children: [
                TextField(controller: ePhone, decoration: const InputDecoration(labelText: '修改電話')),
                const SizedBox(height: 15),
                TextField(controller: eNote, maxLines: 3, decoration: const InputDecoration(labelText: '修改備註', border: OutlineInputBorder())),
                const SizedBox(height: 15),
                const Align(alignment: Alignment.centerLeft, child: Text("歷史紀錄編輯 (每行一筆)：")),
                TextField(controller: eHistory, maxLines: 10, decoration: const InputDecoration(border: OutlineInputBorder(), hintText: "2025-01-01: 內容")),
              ],
            ),
          ),
        ),
        actions: [
          TextButton(onPressed: () => Navigator.pop(ctx), child: const Text("取消")),
          ElevatedButton(
            onPressed: () async {
              final prefs = await SharedPreferences.getInstance();
              int idx = list.indexWhere((c) => c.name == oldData.name);
              if (idx != -1) {
                setState(() {
                  list[idx].phone = ePhone.text.trim();
                  list[idx].note = eNote.text.trim();
                  list[idx].historyLogs = eHistory.text.split('\n').where((s) => s.trim().isNotEmpty).toList();
                });
                await prefs.setStringList('all_customers', list.map((c) => jsonEncode(c.toJson())).toList());
                if (!mounted) return;
                Navigator.pop(ctx);
                ScaffoldMessenger.of(context).showSnackBar(const SnackBar(content: Text("已更新資料")));
              }
            },
            child: const Text("儲存變更"),
          ),
        ],
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('客戶名單總覽'),
        actions: [
          IconButton(icon: const Icon(Icons.file_download, size: 28), onPressed: _downloadBackup, tooltip: '下載備份'),
          const SizedBox(width: 15),
        ],
      ),
      body: Center(
        child: Container(
          constraints: const BoxConstraints(maxWidth: 1000),
          child: list.isEmpty 
            ? const Center(child: Text("目前尚無客戶資料", style: TextStyle(fontSize: 18, color: Colors.grey)))
            : ListView.builder(
                padding: const EdgeInsets.all(20),
                itemCount: list.length,
                itemBuilder: (context, i) {
                  final c = list[i];
                  return Card(
                    elevation: 2,
                    margin: const EdgeInsets.only(bottom: 12),
                    child: ListTile(
                      contentPadding: const EdgeInsets.symmetric(horizontal: 20, vertical: 8),
                      title: Text(c.name, style: const TextStyle(fontWeight: FontWeight.bold, fontSize: 18)),
                      subtitle: Text("電話：${c.phone} | 下次預約：${c.nextDate.isEmpty ? '無' : c.nextDate}"),
                      trailing: const Icon(Icons.edit, color: Colors.amber),
                      onTap: () => _editCustomer(c),
                    ),
                  );
                },
              ),
        ),
      ),
    );
  }
}