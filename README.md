import React, { useState } from 'react';
import InputLabel from '@mui/material/InputLabel';
import MenuItem from '@mui/material/MenuItem';
import FormHelperText from '@mui/material/FormHelperText';
import FormControl from '@mui/material/FormControl';
import Select, { SelectChangeEvent } from '@mui/material/Select';

interface SelectProps {
    label: string;
    value: string;
    onChange: (event: SelectChangeEvent) => void;
    options: { label: string; value: string }[];
    helperText?: string;
    defaultValue?: string; // Add a defaultValue prop
}

const FloatSelect: React.FC<SelectProps> = ({
    label,
    value,
    onChange,
    options,
    helperText,
    defaultValue, // Receive defaultValue from props
}) => {
    return (
        <FormControl sx={{ m: 1, minWidth: 120 }}>
            <InputLabel id={`${label}-label`}>{label}</InputLabel>
            <Select
                labelId={`${label}-label`}
                id={`${label}-select`}
                value={value || defaultValue} // Use defaultValue if value is undefined
                label={label}
                onChange={onChange}
            >
                {options.map((option) => (
                    <MenuItem key={option.value} value={option.value}>
                        {option.label}
                    </MenuItem>
                ))}
            </Select>
            {helperText && <FormHelperText>{helperText}</FormHelperText>}
        </FormControl>
    );
};

export default FloatSelect;

