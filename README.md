# 👗 EvoAI Fashion Assistant

A conversational AI shopping assistant built with multi-step agent architecture, featuring product search, order management, and policy enforcement.

## 🚀 Features

- **Multi-step Agent Pipeline**: Router → Tool Selector → Policy Guard → Responder
- **5+ Integrated Tools**: Product search, size recommendations, ETA calculation, order lookup, cancellation
- **Policy Enforcement**: 60-minute cancellation rule with alternative suggestions
- **Gradio Web Interface**: Clean, accessible chat interface with product gallery
- **Fallback System**: Works with or without external LLM API

## 📋 Quick Start

1. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

2. **Environment Setup**
   ```bash
   cp .env.example .env
   # Add your OPENROUTER_API_KEY (optional - has fallbacks)
   ```

3. **Run Application**
   ```bash
   python src/main.py
   ```

4. **Access Interface**
   - Open `http://localhost:7860` in your browser
   - Try example prompts or ask questions about products/orders

## 🏗️ Architecture

```
User Input → Router → Tool Selector → Policy Guard → Responder → Final Output
```

### Agent Pipeline Steps:
1. **Router**: Classifies user intent (product_assist, order_help, store_info, other)
2. **Tool Selector**: Calls appropriate tools based on intent, collects evidence  
3. **Policy Guard**: Applies business rules (e.g., 60-minute cancellation policy)
4. **Responder**: Generates final response using LLM + collected evidence

## 🛠️ Tools Available

| Tool | Purpose | Example |
|------|---------|---------|
| `product_search` | Find products by query, price, tags | "wedding dresses under $100" |
| `size_recommender` | Suggest sizes based on user input | "I'm between M and L" |
| `eta` | Calculate delivery time by ZIP code | "shipping to 90210" |
| `order_lookup` | Find order by ID + email | "order A1001 for john@example.com" |
| `order_cancel` | Cancel order within policy limits | "cancel order A1003" |

## 📊 Test Examples

### Product Search
```
Input: "Wedding guest, midi, under $120 — I'm between M/L. ETA to 560001?"
Output: Finds 2 dresses, recommends size M/L, provides 4-5 day ETA
```

### Order Cancellation
```
Input: "Cancel order A1003 — email mira@example.com"  
Output: ✅ Success (within 60 minutes)

Input: "Cancel order A1002 — email alex@example.com"
Output: ❌ Denied (over 60 minutes) + alternatives offered
```

## 🎨 Interface Features

- **💬 Chat Assistant**: Main conversational interface with examples
- **🛍️ Product Gallery**: Visual product catalog with images/details  
- **📦 Order Help**: Order management guidance and examples
- **🏪 Store Info**: Policies, contact information, hours

## 📁 Project Structure

```
src/
├── main.py                    # Main Gradio application
├── agent/                     # Agent pipeline components
│   ├── router.py             # Intent classification
│   ├── tools.py              # Tool implementations  
│   ├── policy.py             # Business rule enforcement
│   └── responder.py          # Response generation
└── utils/
    └── openrouter_client.py  # LLM API client

data/
├── products.json             # Product catalog
└── orders.json               # Sample order data

prompts/
└── system_prompt.md          # LLM system instructions

tests/
├── test_agent.py             # Unit tests
└── test_cases.json           # Test scenarios
```

## 🧪 Testing

Run the test suite:
```bash
python -m pytest tests/
```

Test specific scenarios:
```bash
python tests/test_agent.py
```

## 🔧 Configuration

### Environment Variables
- `OPENROUTER_API_KEY`: Optional OpenRouter API key for LLM calls
- Without API key: Uses comprehensive fallback responses

### Customization
- **Products**: Edit `data/products.json`
- **Orders**: Edit `data/orders.json`  
- **Policies**: Modify `src/agent/policy.py`
- **System Prompt**: Update `prompts/system_prompt.md`

## 📈 Production Considerations

### Current Implementation
- ✅ In-memory data storage
- ✅ Rule-based shipping estimates  
- ✅ Simplified order system
- ✅ Basic policy enforcement

### Production Enhancements
- [ ] Database integration (PostgreSQL, MongoDB)
- [ ] Real shipping APIs (UPS, FedEx)
- [ ] Payment processing (Stripe, PayPal)
- [ ] User authentication & sessions
- [ ] Inventory management
- [ ] Analytics & monitoring
- [ ] A/B testing framework

## 🤝 Contributing

1. Fork the repository
2. Create feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m 'Add amazing feature'`
4. Push to branch: `git push origin feature/amazing-feature`
5. Open Pull Request

## 📄 License

This project is licensed under the MIT License - see LICENSE file for details.

## 🆘 Support

- 📧 Email: support@evoai.com
- 📞 Phone: 1-800-EVO-AIHELP
- 🕒 Hours: Monday-Friday 9AM-6PM EST

---

Built with ❤️ using Gradio, OpenRouter, and modern Python practices.
