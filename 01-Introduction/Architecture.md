# PostgreSQL Architecture:
                Client Applications
        (psql, pgAdmin, Node.js, Python)

                      │
                SQL Request
                      │
                      ▼
          +--------------------------+
          | PostgreSQL Server        |
          |                          |
          |  Query Parser            |
          |  Planner/Optimizer       |
          |  Executor                |
          |  Buffer Manager          |
          |  Transaction Manager     |
          |  Storage Manager         |
          +--------------------------+
                      │
                      ▼
          +--------------------------+
          | Data Files (Disk)        |
          | Tables                   |
          | Indexes                  |
          | WAL Logs                 |
          +--------------------------+





# process:
