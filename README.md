import React, { useState } from "react";
import "../../styles/float-select.css";
import {
  FormControl,
  FormHelperText,
  InputLabel,
  MenuItem,
  Select,
  SelectChangeEvent,
} from "@mui/material";
interface Props {
  value: any;
  placeholder?: string; //placeholder text
  styles?: React.CSSProperties; //additional styles object
  handleChange: (event: SelectChangeEvent<HTMLInputElement>) => void;
  // onChange: (event: ChangeEvent<HTMLSelectElement>) => void;
  label?: string; //Label Text
  id?: "selact" | "normal" | "date"; //Type of input field. By default, text
  labelId: string;
  className?: string; //Additional CSS classes for the component
  disabled?: boolean;
  myStyle?: String;
  options: any[];
}
// const [age, setAge] = React.useState<any>("");

export const FloatSelect: React.FC<Props> = ({
  placeholder,
  handleChange,
  label,
  id,
  className,
  styles,
  value,
  disabled,
  myStyle,
  labelId,
  options,
}) => {
  const [focus, setFocus] = useState(false);
  // const selectClass =
  //   focus || (value && value !== 0)
  //     ? "select select-float"
  //     : "select";

  return (
    <div
      className={"float-label " + myStyle}
      onBlur={() => setFocus(false)}
      onFocus={() => setFocus(true)}
    >
      <FormControl style={{ width: "99%", opacity: disabled ? 0.4 : 1 }}>
        <InputLabel
          id="demo-simple-select-helper-label"
          style={{ backgroundColor: "white" }}
        >
          {label}
        </InputLabel>
        <Select
          labelId="demo-simple-select-helper-label"
          id="demo-simple-select-helper"
          value={value}
          label="label"
          className={"input " + className}
          style={styles ? styles : { fontSize: "12px" }}
          disabled={disabled}
          onChange={handleChange}
          onFocus={() => setFocus(true)}
        >
          {options?.map((e: any) => (
            <MenuItem value={e?.value}>{e?.label}</MenuItem>
          ))}
        </Select>
        {/* <FormHelperText>Without label</FormHelperText> */}
      </FormControl>
    </div>
  );
};




<FloatSelect
              labelId={"Work state"}
              options={locationName}
              label="Work state"
              value={state}
              handleChange={(e: any) => {
                setState(e?.target?.value);
                setStateValid(isTextValid(state));
              }}
              styles={{
                border: "1px solid hsl(0, 0%, 80%)",
                textAlign: "left",
                width: "250px",
                height: "40px",
              }}
            />
            {!stateValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {stateError}
              </p>
            ) : null}


            
