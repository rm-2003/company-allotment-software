# Company Allotment Software

### Practice School Management System | Java & Object-Oriented Programming

A console-based internship-allocation application that matches students to company stations using preferences, eligibility, available capacity, and CGPA ordering. Includes separate administrator and student workflows for second-year and final-year allocations.

## At a glance

| Area | Overview |
| --- | --- |
| Resume project | Company Allotment Software |
| Original project name | Practice School Management System (PSMS) |
| Stack | Java, standard-library collections and file I/O |
| Core design | Student subclasses, eligibility interface, generic allocator, state-based menus |
| Data format in this snapshot | CSV inputs and text allotment outputs |
| Context | BITS Pilani CS F213 Object-Oriented Programming, first semester 2022–23 |

## Features

- Administrator menus for managing students, company stations, and allocation rounds.
- Student workflows for preferences, eligibility, offer acceptance/rejection, and withdrawal.
- Second-year and final-year student types with shared student behaviour.
- A generic greedy allocator that considers CGPA order, preferences, eligibility, and station capacity.
- CSV-based student, station, and preference imports; text-based final allotment output.

## How allocation works

1. Reconcile existing accepted, rejected, and withdrawn offers.
2. Sort students in CGPA order.
3. Search each eligible student's preferences for an available station.
4. Preserve accepted offers and record the next round of allotments.

See [Allocator.java](src/Allocator.java) for the implementation. This is the implemented greedy rule, not a claim of globally optimal or stable matching.

## Run locally

Run these commands from the repository root in PowerShell, with a JDK installed:

```powershell
New-Item -ItemType Directory -Path build -Force | Out-Null
$sources = Get-ChildItem src -Filter *.java | Select-Object -ExpandProperty FullName
javac -d build $sources
java -cp build App
```

The application starts with administrator/student menu options. The original academic demo uses `p` as its administrator password; this is a demo convention, not production authentication. Load the supplied CSV files through the administrator workflow before looking up a student. Some output paths use Windows-style separators.

## Project layout

| Path | Contents |
| --- | --- |
| [src/App.java](src/App.java) | Entry point and main menu state machine |
| [src/Admin.java](src/Admin.java) | Administrative workflows and file operations |
| [src/Allocator.java](src/Allocator.java) | Generic allocation algorithm |
| [src/Student.java](src/Student.java) | Shared student model |
| [src/SecondYear.java](src/SecondYear.java), [src/FinalYear.java](src/FinalYear.java) | Student-specific workflows |
| [src/Station.java](src/Station.java), [src/Eligible.java](src/Eligible.java) | Company stations and eligibility contract |
| [src/](src/) | Sample CSV inputs and saved allotment text files |
| [Original README](docs/ORIGINAL_README.md) | Original project/course description |

## Validation

The supplied Java sources compile with JDK 20, and the application starts, displays its menu, and exits using the Exit option. Compilation reports the existing deprecation warning for `Student.finalize()`. Allocation workflows were not exercised end to end.

## Resume fit and limitations

This matches **Company Allotment Software** in the resume and demonstrates object-oriented modelling, shared abstractions, allocation logic, and administrator/student workflows. The resume refers to Excel imports; the supplied implementation reads **CSV files**, which can be exported from Excel. A native `.xlsx` importer is not included here.

This is an academic console prototype with demonstration authentication and file-backed inputs, not a production placement platform. Saved allotments are examples rather than measured allocation-quality results. Compiled classes and editor settings are excluded from the repository.
