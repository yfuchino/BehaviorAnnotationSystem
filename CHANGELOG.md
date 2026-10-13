# Changelog

このプロジェクトのすべての重要な変更を記録しています。

形式は [Keep a Changelog](https://keepachangelog.com/) に準拠し、バージョニングは [Semantic Versioning](https://semver.org/) に従っています。

---

## [Unreleased]

### Added
- i18n support (Japanese/English) for all UI strings
- Per-item edit buttons for behavior customization
- Drag-and-drop reordering of behavior list
- Persistent filename display after file load
- Visible "読込" / "Load" buttons with hidden native file inputs
- Separate JSON save/load for timeline-only data
- Separate JSON save/load for behavior templates
- CSV export with columns: behavior, key, start_sec, end_sec, duration_sec
- Select timeline intervals and delete them individually with the delete button or Delete key; clear selection by clicking the selected interval again or empty timeline space

### Fixed
- Same-file re-selection now triggers change event (input.value cleared after processing)
- Native file input text is hidden; custom filename span displays instead
- Control row vertical alignment improved for better UX

### Changed
- File controls use vertically-centered layout
- Behavior keys are single characters (maxlength=1)
- Enhanced error handling and user alerts

---

## [1.0.0] - 2025-11-25

### Added
- Initial release of Behavior Annotation System (BAS)
- Single-file HTML + CSS + JavaScript application
- Video file loading and playback with playback speed controls
- Behavior definition and recording (Start/Stop intervals)
- Real-time timeline visualization with interval display
- JSON save/load for full state (behaviors + intervals)
- JSON save/load for behavior templates
- JSON save/load for timeline data
- CSV export of completed intervals (behavior, key, start_sec, end_sec, duration_sec)
- Keyboard shortcuts for behavior Start/Stop (by key)
- Click-based Start/Stop for behavior buttons
- i18n support (Japanese / English)
- Edit modal for behavior name/key/color customization
- Responsive design with CSS Flexbox layout
- File input with custom filename display
- MIT License

### Features
- **Video Playback**: Local video file loading, play/pause/stop, speed adjustment (0.1x to 5.0x)
- **Behavior Definition**: Add, edit, delete behaviors with custom colors
- **Timeline Recording**: Record behavior intervals during playback
- **Data Export**: Save to JSON or export to CSV
- **Multi-language**: Switch between Japanese and English UI

---

## Version History

| Version | Date | Status |
|---------|------|--------|
| 1.0.0 | 2025-11-25 | Released |
| Unreleased | TBD | Development |

---

## Notes

- The project is a **single-file application** (`bas.html`). All changes should be made within this file.
- Video files are **not embedded** in save files; users must re-select the same video file when loading saved state.
- Supported video formats depend on the browser; MP4 is widely supported.
- File inputs use internal clearing to support repeated file selection of the same file.

---

## Future Enhancements (Potential)

- [ ] Multi-video project support
- [ ] Undo/Redo functionality
- [ ] More export formats (Excel, Google Sheets integration)
- [ ] Frame-by-frame navigation
- [ ] Annotation drawing tools
- [ ] Batch processing support
- [ ] Database backend for large datasets
- [ ] Mobile/tablet UI optimization

---

更新：2025年11月25日
