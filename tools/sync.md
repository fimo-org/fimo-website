---
label: fimo-sync
icon: sync
---
# fimo-sync (file-mongo-sync)

**fimo-sync** is a flexible and high-performance CLI tool written in Rust for synchronizing documents between two MongoDB collections. It supports both real-time sync via change streams and incremental sync using a chosen field (e.g., `_id`, date).

---

## 🚀 Features

- ✅ Sync at the collection level
- 🔁 Supports MongoDB **Change Streams** with resume token support
- ⏱️ Field-based incremental sync (e.g., date, ObjectId, numeric, string)
- 🧠 Resume file and manual resume value support
- 📦 Batched writes with upsert logic
- 🔐 Full BSON type support (ObjectId, DateTime, Int64, etc.)
- 📁 Multi-mode resume handling with file or CLI-provided values
- 📝 Optional resume type declaration for correct BSON parsing
- 🔄 Compatible with MongoDB 4.0+

---

## 📦 Installation

```bash
cargo install fimo
```

Or clone and build:

```bash
git clone https://github.com/fimo-org/fimo.git
cd fimo
cargo build --release
```

---

## 📝 Usage

### 🔄 Change Stream Mode

```bash
fimo-sync \
  --source-uri mongodb://localhost:27017 \
  --source-db staging \
  --source-collection orders \
  --target-uri mongodb://localhost:27017 \
  --target-db production \
  --target-collection orders_mirror \
  --use-change-stream \
  --resume-file resume.json \
  --store-resume \
  --limit 500
```

### 🕑 Field-Based Sync (e.g., _id or timestamp)

```bash
fimo-sync \
  --sync-field _id \
  --resume-value "64fc40e8e1234567890abcde" \
  --resume-type objectid \
  --resume-file resume.json \
  --store-resume
```

---

## 🔧 CLI Options

| Option               | Description                                              |
|----------------------|----------------------------------------------------------|
| `--source-uri`       | MongoDB URI for source cluster                           |
| `--source-db`        | Source database name                                     |
| `--source-collection`| Source collection name                                   |
| `--target-uri`       | MongoDB URI for target cluster                           |
| `--target-db`        | Target database name                                     |
| `--target-collection`| Target collection name                                   |
| `--use-change-stream`| Use MongoDB change stream for real-time sync            |
| `--sync-field`       | Field to use for incremental sync (e.g. `_id`, `date`)   |
| `--resume-file`      | File path to persist or read resume token/value          |
| `--resume-value`     | Resume value to override file or initialize sync         |
| `--resume-type`      | Type of resume value: `objectid`, `date`, `int`, `string`|
| `--store-resume`     | Enable writing resume value/token after sync             |
| `--limit`            | Maximum number of documents per sync batch               |

---

## 📁 Project Structure

```plaintext
.
├── src/
│   ├── main.rs             # CLI entry point
│   ├── cli.rs              # CLI argument parser
│   ├── sync.rs             # Sync engine
├── examples/               # Sample resume files and use cases
├── tests/                  # Sync test harness
└── Cargo.toml              # Package manifest
```

---

## ⚠️ Disclaimer

**fimo-sync is not affiliated with MongoDB Inc.**  
MongoDB® is a registered trademark of MongoDB Inc.

---

## 📜 License

MIT © fimo.org
