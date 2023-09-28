import React, { ChangeEvent, useState } from "react";
import Grid from "@mui/material/Unstable_Grid2";
import { TextField } from "../../common/TextField/TextField";
import { TextArea } from "../../common/TextArea/TextArea";
import { saveJobData, setJobInputBoxValue } from "../../actions/job";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import { RootState } from "../../redux/store";
import { DropDown } from "../../common/DropDown/DropDown";
import { Button } from "../../common/Button/Button";
import Select from "react-select";
import { isTextValid } from "../../helpers/validate";
import {
  JobTypeList,
  LineOfBusinessList,
  ResumeSourceList,
  WorkTypeList,
} from "../../constants/jobconstants";
import { FloatLabel } from "../../common/FloatLabel/FloatLabel";

interface Props {
  setShowModal: any;
}

const AddJobDetails: React.FC<Props> = ({ setShowModal }) => {
  const dispatch = useAppDispatch();
  const currentJobData = useAppSelector(
    (state: RootState) => state.job.jobData
  );
  const workType = WorkTypeList;
  const jobType = JobTypeList;
  const resumeSource = ResumeSourceList;
  const lineOfBusiness = LineOfBusinessList;

  const [requestIDError, setRequestIDError] = useState<any>();
  const [jobDivaIDError, setJobDivaIDError] = useState<any>();
  const [jobTitleError, setJobTitleError] = useState<any>();
  const [workingFromError, setWorkingFromError] = useState<any>();
  const [workTypeError, setWorkTypeError] = useState<any>();
  const [jobTypeError, setJobTypeError] = useState<any>();
  const [resumeSourceError, setResumeSourceError] = useState<any>();
  const [lineOfBusinessError, setLineOfBusinessError] = useState<any>();
  const [skillSetError, setSkillSetError] = useState<any>();
  const [jobDescriptiontError, setJobDescriptionError] = useState<any>();

  const onValueChange = (key: any, value: any) => {
    dispatch(setJobInputBoxValue(key, value));
  };
  const boxStyle = {
    alignItems: "center",
    border: "none",
    flexGrow: 1,
    marginTop: "3%",
    overflowY: "auto",
    overflowX: "hidden",
    height: "70vh",
    paddingRight: "10px",
    paddingLeft: "10px",
  };

  const [requestIDValid, setRequestIDValid] = useState<boolean>();
  const [jobDivaIDValid, setJobDivaIDValid] = useState<any>();
  const [jobTitleValid, setJobTitleValid] = useState<any>();
  const [jobTypeValid, setJobTypeValid] = useState<any>();
  const [lineOfBusinessValid, setLineOfBusinessValid] = useState<any>();
  const [jobDescriptiontValid, setJobDescriptionValid] = useState<any>();

  function onSubmitClick() {
    setRequestIDValid(isTextValid(currentJobData?.requestID));
    setJobDivaIDValid(isTextValid(currentJobData?.jobDivaID));
    setJobTitleValid(isTextValid(currentJobData?.jobTitle));
    setJobTypeValid(isTextValid(currentJobData?.jobType.value));
    setLineOfBusinessValid(isTextValid(currentJobData?.lineOfBusiness.value));
    setJobDescriptionValid(isTextValid(currentJobData?.jobDescription));
    console.log("setShowModal: ", setShowModal);

    if (
      requestIDValid &&
      jobDivaIDValid &&
      jobTitleValid &&
      jobTypeValid &&
      lineOfBusinessValid &&
      jobDescriptiontValid
    ) {
      dispatch(
        saveJobData(
          currentJobData?.requestID,
          currentJobData?.jobDivaID,
          currentJobData?.jobTitle,
          currentJobData?.jobType.value,
          currentJobData?.lineOfBusiness.value,
          currentJobData?.jobDescription
        )
      );
      setShowModal(false);
    } else {
      if (!requestIDValid) {
        setRequestIDError("Request id is Invalid");
      }
      if (!jobDivaIDValid) {
        setJobDivaIDError("Job diva id is Invalid");
      }
      if (!jobTitleValid) {
        setJobTitleError("Job title is Invalid");
      }
      if (!jobTypeValid) {
        setJobTypeError("Job type is Invalid");
      }
      if (!lineOfBusinessValid) {
        setLineOfBusinessError("Line of business is Invalid");
      }
      if (!jobDescriptiontValid) {
        setJobDescriptionError("Job description is Invalid");
      }
    }
  }

  return (
    <>
      <div className="pt-5 px-5">
        {/* <h1 className="mb-14 ml-5  text-xl font-serif text-center border-solid border-2 block w-[300px] py-3 text-white bg-[#1f7ebc] rounded-lg">
          Job Details
        </h1> */}
        <Grid container spacing={2}>
          <Grid xs={6} md={6}>
            <FloatLabel
              label="*Request Id"
              value={currentJobData?.requestID}
              placeholder={""}
              handleChange={(event) => {
                onValueChange(
                  "requestID",
                  event.target.value.replace(/[^0-9]/gi, "")
                );
                setRequestIDValid(isTextValid(currentJobData?.requestID));
              }}
              className=""
            />
            {!requestIDValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {requestIDError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={6}>
            <FloatLabel
              label="*Job diva ID"
              value={currentJobData?.jobDivaID}
              placeholder={""}
              handleChange={(event) => {
                onValueChange(
                  "jobDivaID",
                  event.target.value.replace(/[^0-9]/gi, "")
                );
                setJobDivaIDValid(isTextValid(currentJobData?.jobDivaID));
              }}
              className=""
            />
            {!jobDivaIDValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {jobDivaIDError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={6}>
            <FloatLabel
              label="*Job title/Position name"
              value={currentJobData?.jobTitle}
              placeholder={""}
              handleChange={(event) => {
                onValueChange(
                  "jobTitle",
                  event.target.value.replace(/[0-9]/gi, "")
                );
                setJobTitleValid(isTextValid(currentJobData?.jobTitle));
              }}
              className=""
            />
            {!jobTitleValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {jobTitleError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={6}>
            {/* <span className="font-serif">Job type</span> */}
            <Select
              placeholder="*Job type"
              className="font-bold text-sm "
              options={jobType}
              value={currentJobData?.jobType}
              getOptionLabel={(option) => option.label}
              getOptionValue={(option) => option.value}
              onChange={(e: any) => {
                onValueChange("jobType", e);
                setJobTypeValid(isTextValid(currentJobData?.jobType.value));
              }}
              // showLabel={false}
            />
            {!jobTypeValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {jobTypeError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={6}>
            {/* <span className="font-serif">Line of Business</span> */}
            <Select
              placeholder="Line of Business"
              className="font-bold text-sm "
              options={lineOfBusiness}
              value={currentJobData?.lineOfBusiness}
              getOptionLabel={(option) => option.label}
              getOptionValue={(option) => option.value}
              onChange={(e: any) => {
                onValueChange("lineOfBusiness", e);
                setLineOfBusinessValid(
                  isTextValid(currentJobData?.lineOfBusiness.value)
                );
              }}
              isSearchable={true}
            />
            {!lineOfBusinessValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {lineOfBusinessError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={6}>
            {/* <span className="font-serif">Job Description</span> */}
            <FloatLabel
              label="Job Description"
              value={currentJobData?.jobDescription}
              placeholder={""}
              handleChange={(event) => {
                onValueChange("jobDescription", event?.target?.value);
                setJobDescriptionValid(
                  isTextValid(currentJobData?.jobDescription)
                );
              }}
              className=""
            />
            {!jobDescriptiontValid ? (
              <p className="" style={{ fontSize: "10px", color: "red" }}>
                {jobDescriptiontError}
              </p>
            ) : null}
          </Grid>
        </Grid>
        <Grid xs={6} md={6}>
          <div className="rate-revision-btn-div  ">
            <Button
              className="submit-btn"
              value="Save & Submit"
              handleClick={() => onSubmitClick()}
            />
          </div>
        </Grid>
      </div>
    </>
  );
};

export default AddJobDetails;
