# GORM ClickHouse Driver

Clickhouse support for GORM

[![test status](https://github.com/go-gorm/clickhouse/workflows/tests/badge.svg?branch=master "test status")](https://github.com/go-gorm/clickhouse/actions)

## Quick Start

You can simply test your connection to your database with the following:

```go
package main

import (
<<<<<<< HEAD
	"github.com/wubin1989/clickhouse"
	"github.com/wubin1989/gorm"
=======
	"gorm.io/driver/clickhouse"
	"gorm.io/gorm"
>>>>>>> 065c557faa017e4b7c68dd8eeaced0bbad937403
)

type User struct {
	Name string
	Age  int
}

func main() {
	dsn := "clickhouse://gorm:gorm@localhost:9942/gorm?dial_timeout=10s&read_timeout=20s"
	db, err := gorm.Open(clickhouse.Open(dsn), &gorm.Config{})
	if err != nil {
		panic("failed to connect database")
	}

	// Auto Migrate
	db.AutoMigrate(&User{})
	// Set table options
	db.Set("gorm:table_options", "ENGINE=Distributed(cluster, default, hits)").AutoMigrate(&User{})

	// Set table cluster options
	db.Set("gorm:table_cluster_options", "on cluster default").AutoMigrate(&User{})

	// Insert
	db.Create(&User{Name: "Angeliz", Age: 18})

	// Select
	db.Find(&User{}, "name = ?", "Angeliz")

	// Batch Insert
	user1 := User{Age: 12, Name: "Bruce Lee"}
	user2 := User{Age: 13, Name: "Feynman"}
	user3 := User{Age: 14, Name: "Angeliz"}
	var users = []User{user1, user2, user3}
	db.Create(&users)
	// ...
}

```

## Advanced Configuration

```go
package main

import (
  std_ck "github.com/ClickHouse/clickhouse-go/v2"
<<<<<<< HEAD
  "github.com/wubin1989/clickhouse"
  "github.com/wubin1989/gorm"
=======
  "gorm.io/driver/clickhouse"
  "gorm.io/gorm"
>>>>>>> 065c557faa017e4b7c68dd8eeaced0bbad937403
)

sqlDB, err := std_ck.OpenDB(&std_ck.Options{
	Addr: []string{"127.0.0.1:9999"},
	Auth: std_ck.Auth{
		Database: "default",
		Username: "default",
		Password: "",
	},
	TLS: &tls.Config{
		InsecureSkipVerify: true,
	},
	Settings: std_ck.Settings{
		"max_execution_time": 60,
	},
	DialTimeout: 5 * time.Second,
	Compression: &std_ck.Compression{
		std_ck.CompressionLZ4,
	},
	Debug: true,
})

func main() {
  db, err := gorm.Open(clickhouse.New(click.Config{
    Conn: sqlDB, // initialize with existing database conn
  })
}
```

```go
package main

import (
<<<<<<< HEAD
  "github.com/wubin1989/clickhouse"
  "github.com/wubin1989/gorm"
=======
  "gorm.io/driver/clickhouse"
  "gorm.io/gorm"
>>>>>>> 065c557faa017e4b7c68dd8eeaced0bbad937403
)

// refer to https://github.com/ClickHouse/clickhouse-go
var dsn = "clickhouse://username:password@host1:9000,host2:9000/database?dial_timeout=200ms&max_execution_time=60"

func main() {
  db, err := gorm.Open(clickhouse.New(click.Config{
    DSN: dsn,
    Conn: conn,                       // initialize with existing database conn
    DisableDatetimePrecision: true,   // disable datetime64 precision, not supported before clickhouse 20.4
    DontSupportRenameColumn: true,    // rename column not supported before clickhouse 20.4
    DontSupportEmptyDefaultValue: false,  // do not consider empty strings as valid default values
    SkipInitializeWithVersion: false, // smart configure based on used version
    DefaultGranularity: 3,            // 1 granule = 8192 rows
    DefaultCompression: "LZ4",        // default compression algorithm. LZ4 is lossless
    DefaultIndexType: "minmax",       // index stores extremes of the expression
    DefaultTableEngineOpts: "ENGINE=MergeTree() ORDER BY tuple()",
  }), &gorm.Config{})
}
```

<<<<<<< HEAD
Checkout [https://github.com/wubin1989](https://github.com/wubin1989) for details.
=======
Checkout [https://gorm.io](https://gorm.io) for details.
>>>>>>> 065c557faa017e4b7c68dd8eeaced0bbad937403
