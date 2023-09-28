import React, { useEffect, useState } from "react";
import "./CandidateDetails.css";
import Grid from "@mui/material/Unstable_Grid2";
import { TextField } from "../../common/TextField/TextField";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import { RootState } from "../../redux/store";
import { setCandidateInputBoxValue } from "../../actions/candidate";
import { DropDown } from "../../common/DropDown/DropDown";
import {
  LocationName,
  WorkAuthorization,
} from "../../constants/candidateclientconstants";
import Select from "react-select";
import { yesNoList } from "../../constants/constants";
import { isTextValid } from "../../helpers/validate";

// interface Props {
//     nextButtonClick: any;
//     setNextButtonClick: any;
//     setValid: any;
//     valid: any;
// }

const CandidateDetails: React.FC = () => {
  // setNextButtonClick(false);
  // setValid(false);

  const dispatch = useAppDispatch();
  const currentCandidateData = useAppSelector(
    (state: RootState) => state.candidate.candidateData
  );
  let workAuthorizationData = useAppSelector(
    (state: RootState) => state.workAuthorization.allWorkAuthorizationData
  );
  var result: any = [];
  if (workAuthorizationData != undefined) {
    workAuthorizationData.forEach((element: { workAuthorization: any }) => {
      result.push({
        label: element.workAuthorization,
        value: element.workAuthorization,
      });
    });
  }
  const locationName = LocationName;
  // const workAuthorization = WorkAuthorization;

  const onValueChange = (key: any, value: any) => {
    dispatch(setCandidateInputBoxValue(key, value));
  };

  // useEffect(() => {
  //     console.log('nextButtonClick: out if ', nextButtonClick);
  //     if (nextButtonClick) {
  //         console.log('nextButtonClick: ', nextButtonClick);
  //         if (validateFirstName()) {
  //             console.log("jrlll");

  //             setValid(true);
  //             console.log('validateFirstName: ', valid);
  //         }

  //     }
  //     // setNextButtonClick(false);
  // }, [nextButtonClick, valid])

  // const validateFirstName = () => {
  //     setFirstNameValid(isTextValid(currentCandidateData?.firstName));
  //     if (!firstNameValid) {
  //         console.log('firstNameValid: if ', firstNameValid);
  //         setFirstNameError('First name is required');
  //         return false;
  //     }
  //     console.log('firstNameValid: else ', firstNameValid);
  //     setFirstNameError('');
  //     return true;
  // };

  // const validateMiddleName = () => {
  //     if (!firstNameValid) {
  //         setFirstNameError('First name is required');
  //         return false;
  //     }
  //     setFirstNameError('');
  //     return true;
  // };

  const [firstNameError, setFirstNameError] = useState<any>();
  const [middleNameError, setMiddleNameError] = useState<any>();
  const [lastNameError, setLastNameError] = useState<any>();
  const [line1Error, setLine1Error] = useState<any>();
  const [line2Error, setLine2Error] = useState<any>();
  const [cityError, setCityError] = useState<any>();
  const [stateError, setStateError] = useState<any>();
  const [zipCodeError, setZipCodeError] = useState<any>();
  const [countryError, setCountryError] = useState<any>();
  const [emailError, setEmailError] = useState<any>();
  const [contactNumberError, setContactNumberError] = useState<any>();
  const [workAuthorizationError, setWorkAuthorizationError] = useState<any>();
  const [
    workAuthorizationExpiryDateError,
    setWorkAuthorizationExpiryDateError,
  ] = useState<any>();

  const [firstNameValid, setFirstNameValid] = useState<boolean>(false);
  const [middleNameValid, setMiddleNameValid] = useState<boolean>();
  const [lastNameValid, setLastNameValid] = useState<boolean>();
  const [line1Valid, setLine1Valid] = useState<boolean>();
  const [line2Valid, setLine2Valid] = useState<boolean>();
  const [cityValid, setCityValid] = useState<boolean>();
  const [stateValid, setStateValid] = useState<boolean>();
  const [zipCodeValid, setZipCodeValid] = useState<boolean>();
  const [countryValid, setCountryValid] = useState<boolean>();
  const [emailValid, setEmailValid] = useState<boolean>();
  const [contactNumberValid, setContactNumberValid] = useState<boolean>();
  const [workAuthorizationValid, setWorkAuthorizationValid] =
    useState<boolean>();
  const [
    workAuthorizationExpiryDateValid,
    setWorkAuthorizationExpiryDateValid,
  ] = useState<boolean>();

  function validateFields() {
    if (!firstNameValid) {
      setFirstNameError("First name is invalid");
    }
    if (!middleNameValid) {
      setMiddleNameError("Middle name is invalid");
    }
    if (!lastNameValid) {
      setLastNameError("Last name is invalid");
    }
    if (!line1Valid) {
      setLine1Error("Line 1 is invalid");
    }
    if (!line2Valid) {
      setLine2Error("Line 2 is invalid");
    }
    if (!cityValid) {
      setCityError("City is invalid");
    }
    if (!stateValid) {
      setStateError("State is invalid");
    }
    if (!zipCodeValid) {
      setZipCodeError("Zip code is invalid");
    }
    if (!countryValid) {
      setCountryError("Country is invalid");
    }
    if (!emailValid) {
      setEmailError("Email is invalid");
    }
    if (!contactNumberValid) {
      setContactNumberError("Contact number is invalid");
    }
    if (!workAuthorizationValid) {
      setWorkAuthorizationError("Work authorization is invalid");
    }
    if (!workAuthorizationExpiryDateValid) {
      setWorkAuthorizationError("Work authorization is invalid");
    }
  }

  return (
    <>
      Candidate details
      <div className="flex gap-5 " style={{ margin: "auto", width: "100%" }}>
        <div className="relative w-[100%] mt-10 border border-solid">
          <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400">
            <thead className="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
              <tr>
                <th scope="col" className="px-6 py-3">
                  {/* <span>Client name</span> */}
                </th>
                <th></th>
              </tr>
            </thead>
            <tbody>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Candidate first name</span>
                </td>
                <td className="px-6 py-0">
                  {!firstNameValid ? (
                    <p className="" style={{ fontSize: "12px", color: "red" }}>
                      {firstNameError}
                    </p>
                  ) : null}
                  <TextField
                    value={currentCandidateData?.firstName}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("firstName", event?.target?.value);
                      // validateFirstName();
                    }}
                    className=""
                    // handleBlur={validateFirstName}
                  />
                  {/* {!firstNameValid ? (
                                        <p className="" style={{ fontSize: "12px", color: "red" }}>{firstNameError}</p>
                                    ) : null} */}
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Candidate middle name</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentCandidateData?.middleName}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("middleName", event?.target?.value);
                    }}
                    className=""
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Candidate last name</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentCandidateData?.lastName}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("lastName", event?.target?.value);
                    }}
                    className=""
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Line 1</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentCandidateData?.line1}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("line1", event?.target?.value);
                    }}
                    className=""
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Line 2</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentCandidateData?.line2}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("line2", event?.target?.value);
                    }}
                    className=""
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>City</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentCandidateData?.city}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("city", event?.target?.value);
                    }}
                    className=""
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>State</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={locationName}
                    value={currentCandidateData?.state}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("state", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
            </tbody>
          </table>
        </div>
        <div className="relative w-[100%] mt-10 border border-solid">
          <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400">
            <thead className="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400"></thead>
            <tbody className=" font-serif">
              <tr className="bg-white  dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  {/* <span>Candidate first name</span> */}
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Zip code</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentCandidateData?.zipCode}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("zipCode", event?.target?.value);
                    }}
                    className=""
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Country</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentCandidateData?.country}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("country", event?.target?.value);
                    }}
                    className=""
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Candidate email address</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentCandidateData?.email}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("email", event?.target?.value);
                    }}
                    className=""
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Candidate contact no.</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentCandidateData?.contactNumber}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("contactNumber", event?.target?.value);
                    }}
                    className=""
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Work authorization</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    // options={workAuthorization}
                    options={yesNoList}
                    value={currentCandidateData?.workAuthorization}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("workAuthorization", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Work authorization expiry date</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentCandidateData?.workAuthorizationExpiryDate}
                    type="date"
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange(
                        "workAuthorizationExpiryDate",
                        event?.target?.value
                      );
                    }}
                    className=""
                  />
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </>
  );
};

export default CandidateDetails;
