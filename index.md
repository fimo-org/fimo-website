# 🧩 fimo: File Mongo Data Tools

**Fimo** is a modular, Rust-based CLI toolkit for high-performance MongoDB workflows — including large-scale imports, streaming sync, and intelligent upserts.

---

## ⚠️ Disclaimer

**Fimo is an independent open-source project and is not affiliated with MongoDB Inc.**  
MongoDB® and the MongoDB leaf logo are registered trademarks of MongoDB Inc.  
Use of the MongoDB name does not imply endorsement by MongoDB Inc.

---


## 📥 fimo-csv

`fimo-csv` is a robust CSV-to-MongoDB loader. It supports:

- ✅ YAML-based field mappings
- ✅ Type conversion to BSON (ObjectId, DateTime, Decimal128, etc.)
- ✅ MiniJinja templating for flexible insert/update/upsert payloads
- ✅ Batch mode, dry-run, and validate-only options
- ✅ Custom delimiter, quote, and date format support

---

## 🔄 fimo-sync

`fimo-sync` is a high-performance tool for synchronizing documents between two MongoDB collections. It supports:

- ✅ **Change Stream-based sync** with resume token support
- ✅ **Field-based sync** (e.g. ObjectId, timestamp, etc.) using `$gt` comparison
- ✅ **Batch writes** for efficiency
- ✅ **Resume file persistence**
- ✅ Support for `ObjectId`, `Date`, `String`, `Int64` resume values

---

## 📦 Download

You can build from source:

```bash
git clone https://github.com/fimo-org/fimo.git
cd fimo
cargo build --release
```

Or install from crates.io:

```bash
cargo install fimo
```

---

## 🛠 Examples

### fimo-csv 

```bash
fimo-csv \
  --input orders.csv \
  --mapping mapping.yaml \
  --mongo-uri mongodb://localhost:27017 \
  --db analytics \
  --collection orders \
  --operation upsert \
  --template-dir templates \
  --extended-json
```

### fimo-sync (change stream)

```bash
fimo-sync \
  --source-uri mongodb://localhost:27017 \
  --source-db source_db \
  --source-collection source_col \
  --target-uri mongodb://localhost:27017 \
  --target-db target_db \
  --target-collection target_col \
  --use-change-stream \
  --resume-file resume.json \
  --store-resume \
  --limit 500
```

### fimo-sync (field-based)

```bash
fimo-sync \
  --sync-field _id \
  --resume-value "64fc40e8e1234567890abcde" \
  --resume-type objectid \
  --store-resume \
  --resume-file resume.json
```

---

## 📁 Repository

- [Source Code on GitHub](https://github.com/fimo-org/fimo)
- [Issues & Contributions](https://github.com/fimo-org/fimo/issues)

---

© 2024 fimo.org — Rust ❤️ MongoDB

