import React, { useEffect, useState } from "react";
import Grid from "@mui/material/Unstable_Grid2";
import { TextField } from "../../common/TextField/TextField";
import { Button } from "../../common/Button/Button";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import { RootState } from "../../redux/store";
import {
  saveContractTypeData,
  setContractTypeInputBoxValue,
} from "../../actions/contractType";
import { isTextValid } from "../../helpers/validate";
import { FloatLabel } from "../../common/FloatLabel/FloatLabel";
interface Props {
  setShowModal: any;
  data: any;
}
const EditContractType: React.FC<Props> = ({ setShowModal }) => {
  const dispatch = useAppDispatch();
  const contractType = useAppSelector(
    (state: RootState) => state.contractType.contractTypeData
  );

  const onContractTypeValueChange = (key: any, value: any) => {
    dispatch(setContractTypeInputBoxValue(key, value));
  };

  const [contractTypeError, setContractTypeError] = useState<any>();

  const [contractTypeValid, setContractTypeValid] = useState<boolean>();

  useEffect(() => {
    setContractTypeValid(isTextValid(contractType?.contractType));
  }, [contractType]);

  function onSubmitClick() {
    setContractTypeValid(isTextValid(contractType?.contractType));
    if (contractTypeValid) {
      dispatch(saveContractTypeData(contractType?.contractType));
      setShowModal(false);
    } else {
      if (!contractTypeValid) {
        setContractTypeError("Contract type is invalid");
        setShowModal(false);
      }
    }
  }

  return (
    <>
      {/* <h2>Contract type</h2> */}
      <div className="pt-5 px-5">
        <Grid container spacing={2}>
          <Grid xs={12} md={12}>
            <FloatLabel
              label="*Contract type"
              value={contractType?.contractType}
              placeholder={""}
              handleChange={(event) => {
                onContractTypeValueChange("contractType", event.target.value);
              }}
              className=""
            />
            {!contractTypeValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {contractTypeError}
              </p>
            ) : null}
          </Grid>
        </Grid>
        <Grid xs={6} md={6}>
          <div className="rate-revision-btn-div">
            <Button
              className="submit-btn"
              value="Update ContractType"
              handleClick={() => onSubmitClick()}
            />
          </div>
        </Grid>
      </div>
    </>
  );
};

export default EditContractType;
