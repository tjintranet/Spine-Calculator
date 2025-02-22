# Book Spine Calculator

A web-based calculator for determining book spine width based on page count, paper specifications, and binding style.

## Overview

The spine calculator uses three main factors to determine spine width:
1. Number of pages
2. Paper specifications (grammage and volume)
3. Binding style and board thickness (for cased binding)

## Modifying Paper Specifications

Paper specifications are stored in the `PAPER_SPECS` object at the top of the script section. Each paper type has three properties:
- `name`: Display name shown in dropdown
- `grammage`: Paper weight in gsm
- `volume`: Paper volume factor

### Adding a New Paper Type

To add a new paper type, add a new entry to the `PAPER_SPECS` object:

```javascript
PAPER_SPECS = {
    // Existing paper types...
    
    new_paper_key: {
        name: 'Display Name for Paper',
        grammage: 80,  // Paper weight in gsm
        volume: 15     // Paper volume factor
    }
}
```

Then add a corresponding option to the HTML select element:

```html
<select class="form-select" id="paperType">
    <!-- Existing options... -->
    <option value="new_paper_key">Display Name for Paper</option>
</select>
```

### Removing a Paper Type

To remove a paper type:
1. Delete the entry from the `PAPER_SPECS` object
2. Remove the corresponding option from the paperType select element

## Modifying Board Thicknesses

Board thicknesses for cased binding are defined in the HTML select element with ID 'boardThickness'.

### Adding a New Board Thickness

Add a new option to the boardThickness select element:

```html
<select class="form-select" id="boardThickness">
    <!-- Existing options... -->
    <option value="2.0">2.0 mm</option>
</select>
```

### Removing a Board Thickness

Simply remove the corresponding option from the boardThickness select element.

## Calculation Formula

The spine width is calculated using the following formula:

For Limp binding:
```
spine_width = (pages * grammage * volume) / 20000
```

For Cased binding:
```
spine_width = (pages * grammage * volume) / 20000 + board_thickness + 0.50
```

## Validation

The calculator includes validation for:
- Required fields (pages, paper type, binding style)
- Board thickness selection for cased binding
- Maximum spine width warning (60mm limit)

## Dependencies

The calculator uses:
- Bootstrap 5.3.2 for styling
- Bootstrap Icons for icons

## Troubleshooting

If calculations seem incorrect, verify:
1. Paper specifications in the `PAPER_SPECS` object
2. Board thickness values in the select element
3. The spine calculation formula constants (20000 divisor, 0.50 addition for cased)