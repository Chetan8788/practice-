import React, { useState } from "react";
import Grid from "@mui/material/Unstable_Grid2";
import { TextField } from "../../common/TextField/TextField";
import { Button } from "../../common/Button/Button";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import { RootState } from "../../redux/store";
import {
  saveWorkAuthorizationData,
  setWorkAuthorizationInputBoxValue,
} from "../../actions/workAuthorization";
import { isTextValid } from "../../helpers/validate";
import { FloatLabel } from "../../common/FloatLabel/FloatLabel";
interface Props {
  setShowModal: any;
  data: any;
}
const EditWorkAuthorization: React.FC<Props> = ({ setShowModal }) => {
  const dispatch = useAppDispatch();
  const workAuthorization = useAppSelector(
    (state: RootState) => state.workAuthorization.workAuthorizationData
  );

  const onWorkAuthorizationValueChange = (key: any, value: any) => {
    dispatch(setWorkAuthorizationInputBoxValue(key, value));
  };

  const [workAuthorizationError, setWorkAuthorizationError] = useState<any>();

  const [workAuthorizationValid, setWorkAuthorizationValid] =
    useState<boolean>();

  function onSubmitClick() {
    setWorkAuthorizationValid(
      isTextValid(workAuthorization?.workAuthorization)
    );
    console.log("setShowModal: ", setShowModal);
    if (workAuthorizationValid) {
      console.log("called");
      dispatch(saveWorkAuthorizationData(workAuthorization?.workAuthorization));
      setShowModal(false);
    } else {
      if (!workAuthorizationValid) {
        setWorkAuthorizationError("Work authorization is invalid");
        setShowModal(false);
      }
    }
  }

  return (
    <>
      {/* <h2>Work authorization</h2> */}
      <div className="pt-5 px-5">
        <Grid container spacing={2}>
          <Grid xs={12} md={12}>
            <FloatLabel
              label="*Work authorization type"
              value={workAuthorization?.workAuthorization}
              placeholder={""}
              handleChange={(event) => {
                onWorkAuthorizationValueChange(
                  "workAuthorization",
                  event.target.value
                );
              }}
              className=""
            />
            {!workAuthorizationValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {workAuthorizationError}
              </p>
            ) : null}
          </Grid>
        </Grid>
        <Grid xs={12} md={12}>
          <div className="rate-revision-btn-div">
            <Button
              className="submit-btn"
              value="Update WorkAuthorization"
              handleClick={() => onSubmitClick()}
            />
          </div>
        </Grid>
      </div>
    </>
  );
};

export default EditWorkAuthorization;
