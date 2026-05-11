# Design Review Notes

## Review Items

- [ ] Requirements defined
- [ ] Architecture reviewed
- [ ] Power modes reviewed
- [ ] Connector suitability reviewed
- [ ] Schematic ERC checked
- [ ] PCB DRC checked
- [ ] Footprints checked against datasheets
- [ ] JST mating connectors selected
- [ ] BOM reviewed
- [ ] Stack-up defined
- [ ] Manufacturing outputs generated
- [ ] Bring-up plan prepared

## Key Risks

1. Camera charging behavior through dummy battery path must be bench-verified.
2. Firmware must prevent simultaneous 8V and battery path enable.
3. JST connector orientation and mating access must be verified inside housing.
4. DRV8825 thermal behavior must be validated under motor operation.
5. Sensor noise should be checked during motor movement.
