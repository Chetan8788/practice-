import React, { useState } from 'react';
import Grid from '@mui/material/Unstable_Grid2';
import { TextField } from '../../common/TextField/TextField';
import { saveClientData, setClientInputBoxValue } from '../../actions/client';
import { ContractType, LocationName } from '../../constants/candidateclientconstants';
import { useAppDispatch, useAppSelector } from '../../hooks/app';
import { RootState } from '../../redux/store';
import { Box } from '@mui/material';
import { Button } from '../../common/Button/Button';
import { useNavigate } from 'react-router-dom';
import { addClientStateList } from '../../constants/constants';
import { isEmailValid, isMobileNumberValid, isNumberValid, isTextValid } from '../../helpers/validate';
import { EMPTY_ADDRESS_DATA } from '../../utils/addressutil';
import Select from 'react-select';
import { FloatLabel } from '../../common/FloatLabel/FloatLabel';

interface Props {
    setShowModal: any,
}

const AddClientDetails: React.FC<Props> = ({ setShowModal }) => {
    const dispatch = useAppDispatch();
    const currentClientData = useAppSelector((state: RootState) => state.client.clientData);
    const allClientData = useAppSelector((state: RootState) => state.client.allClientData);
    let allClientName: object[] = [];
    // if (allClientData.length !== 0) {
    //     allClientData.map((
    //         a: { clientName: string; address: typeof EMPTY_ADDRESS_DATA[] }
    //     ) => {
    //         a.address.map((
    //             b: { city: string; state: string; }
    //         ) => {
    //             let data = {
    //                 value: a.clientName + " (" + b.city + "/" + b.state + ")",
    //                 label: a.clientName + " (" + b.city + "/" + b.state + ")"
    //             }
    //             allClientName.push(data);
    //         });
    //     })
    // }
    const locationName = LocationName;


    const [clientNameError, setClientNameError] = useState<any>();
    const [endClientNameError, setEndClientNameError] = useState<any>();
    const [mspNameError, setMspNameError] = useState<any>();
    const [line1Error, setLine1Error] = useState<any>();
    const [line2Error, setLine2Error] = useState<any>();
    const [cityError, setCityError] = useState<any>();
    const [stateError, setStateError] = useState<any>();
    const [zipCodeError, setZipCodeError] = useState<any>();
    const [countryError, setCountryError] = useState<any>();
    const [emailError, setEmailError] = useState<any>();
    const [contactError, setContactError] = useState<any>();
    const [faxError, setFaxError] = useState<any>();


    const onValueChange = (key: any, value: any) => {
        dispatch(setClientInputBoxValue(key, value));
    };

    const boxStyle = {
        alignItems: 'center',
        border: 'none', flexGrow: 1,
        marginTop: "3%", overflowY: "auto",
        overflowX: 'hidden',
        height: "70vh",
        paddingRight: "10px",
        paddingLeft: "10px"
    }

    const [clientNameValid, setClientNameValid] = useState<boolean>();
    const [endClientNameValid, setEndClientNameValid] = useState<boolean>();
    const [mspNameValid, setMspNameValid] = useState<boolean>();
    const [line1Valid, setLine1Valid] = useState<boolean>();
    const [line2Valid, setLine2Valid] = useState<boolean>();
    const [cityValid, setCityValid] = useState<boolean>();
    const [stateValid, setStateValid] = useState<boolean>();
    const [zipCodeValid, setZipCodeValid] = useState<boolean>();
    const [countryValid, setCountryValid] = useState<boolean>();
    const [emailValid, setEmailValid] = useState<boolean>();
    const [contactValid, setContactValid] = useState<boolean>();
    const [faxValid, setFaxValid] = useState<boolean>();

    function onSubmitClick() {
        setClientNameValid(isTextValid(currentClientData?.clientName));
        setEndClientNameValid(isTextValid(currentClientData?.endClientName));
        setMspNameValid(isTextValid(currentClientData?.mspName));
        setLine1Valid(isTextValid(currentClientData?.line1));
        setLine2Valid(isTextValid(currentClientData?.line2));
        setCityValid(isTextValid(currentClientData?.city));
        setStateValid(isTextValid(currentClientData?.state.value));
        setZipCodeValid(isTextValid(currentClientData?.zipCode));
        setCountryValid(isTextValid(currentClientData?.country));
        setEmailValid(isEmailValid(currentClientData?.email));
        setContactValid(isTextValid(currentClientData?.contactNumber));
        setFaxValid(isTextValid(currentClientData?.faxNumber));

        console.log('setShowModal: ', setShowModal);
        if (clientNameValid && endClientNameValid && mspNameValid && line1Valid && line2Valid && cityValid
            && stateValid && countryValid && emailValid && zipCodeValid && contactValid && faxValid) {

            dispatch(saveClientData(
                currentClientData?.clientName,
                currentClientData?.endClientName,
                currentClientData?.mspName,
                currentClientData?.email,
                currentClientData?.contactNumber,
                currentClientData?.faxNumber,
                currentClientData?.line1,
                currentClientData?.line2,
                currentClientData?.city,
                currentClientData?.state.value,
                currentClientData?.zipCode,
                currentClientData?.country
            ));
            setShowModal(false);
        } else {
            if (!clientNameValid) {
                setClientNameError("Client name is Invalid")
            }
            if (!endClientNameValid) {
                setEndClientNameError("End client name is Invalid")
            }
            if (!mspNameValid) {
                setMspNameError("Msp name is Invalid")
            }
            if (!line1Valid) {
                setLine1Error("Line 1 is Invalid")
            }
            if (!line2Valid) {
                setLine2Error("Line 2 is Invalid")
            }
            if (!cityValid) {
                setCityError("City is Invalid")
            }
            if (!stateValid) {
                setStateError("State is Invalid")
            }
            if (!zipCodeValid) {
                setZipCodeError("Zip code is Invalid");
            }
            if (!countryValid) {
                setCountryError("Country is Invalid");
            }
            if (!emailValid) {
                setEmailError("Email is Invalid");
            }
            if (!contactValid) {
                setContactError("Contact is Invalid");
            }
            if (!faxValid) {
                setFaxError("Fax no is Invalid");
            }
        }
    }

    return (
        <>
            {/* <Box sx={boxStyle}> */}
            {/* <h6>Client details</h6> */}
            <div className="pt-5 px-5">
                <Grid container spacing={2}>
                    <Grid xs={6} md={6}>
                        <FloatLabel
                            label='*Client name'
                            value={currentClientData?.clientName}
                            placeholder={""}
                            handleChange={(event) => {
                                onValueChange("clientName", event.target.value.replace(/[0-9]/gi, ""));
                            }}
                            className=""
                        />
                        {!clientNameValid ? (
                            <p className="" style={{ fontSize: "12px", color: "red" }}>{clientNameError}</p>
                        ) : null}
                    </Grid>
                    <Grid xs={6} md={6}>
                        <FloatLabel
                            label='*End client name'
                            value={currentClientData?.endClientName}
                            placeholder={""}
                            handleChange={(event) => {
                                onValueChange("endClientName", event.target.value.replace(/[0-9]/gi, ""));
                            }}
                            className=""
                        />
                        {!endClientNameValid ? (
                            <p className="" style={{ fontSize: "12px", color: "red" }}>{endClientNameError}</p>
                        ) : null}
                    </Grid>
                    <Grid xs={6} md={6}>
                        <FloatLabel
                            label='*MSP name'
                            value={currentClientData?.mspName}
                            placeholder={""}
                            handleChange={(event) => {
                                onValueChange("mspName", event.target.value.replace(/[0-9]/gi, ""));
                            }}
                            className=""
                        />
                        {!mspNameValid ? (
                            <p className="" style={{ fontSize: "12px", color: "red" }}>{mspNameError}</p>
                        ) : null}
                    </Grid>
                    <Grid xs={6} md={6}>
                        <FloatLabel
                            label='*Email'
                            value={currentClientData?.email}
                            placeholder={""}
                            handleChange={(event) => {
                                onValueChange("email", event.target.value.replace(/\s/g, ""));
                            }}
                            className=""
                        />
                        {!emailValid ? (
                            <p className="" style={{ fontSize: "12px", color: "red" }}>{emailError}</p>
                        ) : null}
                    </Grid>
                    <Grid xs={6} md={6}>
                        <FloatLabel
                            label='*Contact number'
                            value={currentClientData?.contactNumber}
                            placeholder={""}
                            handleChange={(event) => {
                                onValueChange("contactNumber", event.target.value.replace(/[^0-9]/gi, ""));
                                setContactValid(currentClientData?.contactNumber)
                            }}
                            className=""
                        />
                        {!contactValid ? (
                            <p className="" style={{ fontSize: "12px", color: "red" }}>{contactError}</p>
                        ) : null}
                    </Grid>
                    <Grid xs={6} md={6}>
                        <FloatLabel
                            label='*Fax number'
                            value={currentClientData?.faxNumber}
                            placeholder={""}
                            handleChange={(event) => {
                                onValueChange("faxNumber", event.target.value.replace(/[^0-9]/gi, ""));
                                setFaxValid(currentClientData?.faxNumber)
                            }}
                            className=""
                        />
                        {!faxValid ? (
                            <p className="" style={{ fontSize: "12px", color: "red" }}>{faxError}</p>
                        ) : null}
                    </Grid>
                    {/* currentClientData?.email,
                    currentClientData?.contactNumber,
                    currentClientData?.faxNumber, */}
                    <Grid xs={6} md={6}>
                        <FloatLabel
                            label='*Address line 1'
                            value={currentClientData?.line1}
                            placeholder={""}
                            handleChange={(event) => {
                                onValueChange("line1", event?.target?.value);
                            }}
                            className=""
                        />
                        {!line1Valid ? (
                            <p className="" style={{ fontSize: "12px", color: "red" }}>{line1Error}</p>
                        ) : null}
                    </Grid>
                    <Grid xs={6} md={6}>
                        <FloatLabel
                            label='*Address line 2'
                            value={currentClientData?.line2}
                            placeholder={""}
                            handleChange={(event) => {
                                onValueChange("line2", event?.target?.value);
                            }}
                            className=""
                        />
                        {!line2Valid ? (
                            <p className="" style={{ fontSize: "12px", color: "red" }}>{line2Error}</p>
                        ) : null}
                    </Grid>
                    <Grid xs={6} md={6}>
                        <FloatLabel
                            label='*City'
                            value={currentClientData?.city}
                            placeholder={""}
                            handleChange={(event) => {
                                onValueChange("city", event.target.value.replace(/[0-9]/gi, ""));
                            }}
                            className=""
                        />
                        {!cityValid ? (
                            <p className="" style={{ fontSize: "12px", color: "red" }}>{cityError}</p>
                        ) : null}
                    </Grid>
                    <Grid xs={6} md={6}>
                        <Select
                            placeholder="Work state"
                            options={locationName}
                            value={currentClientData?.state}
                            getOptionLabel={(option) => option.label}
                            getOptionValue={(option) => option.value}
                            onChange={(e: any) => {
                                onValueChange("state", e);
                            }}
                            isSearchable={true}
                        />
                        {!stateValid ? (
                            <p className="" style={{ fontSize: "12px", color: "red" }}>{stateError}</p>
                        ) : null}
                    </Grid>
                    <Grid xs={6} md={6}>
                        <FloatLabel
                            label='*Zip code'
                            value={currentClientData?.zipCode}
                            placeholder={""}
                            handleChange={(event) => {
                                onValueChange("zipCode", event.target.value.replace(/[^0-9]/gi, ""));
                            }}
                            className=""
                        />
                        {!zipCodeValid ? (
                            <p className="" style={{ fontSize: "12px", color: "red" }}>{zipCodeError}</p>
                        ) : null}
                    </Grid>
                    <Grid xs={6} md={6}>
                        {/* <span>*Client country</span> */}
                        <FloatLabel
                            label='*Client country'
                            value={currentClientData?.country}
                            placeholder={""}
                            handleChange={(event) => {
                                onValueChange("country", event.target.value.replace(/[0-9]/gi, ""));
                            }}
                            className=""
                        />
                        {!countryValid ? (
                            <p className="" style={{ fontSize: "12px", color: "red" }}>{countryError}</p>
                        ) : null}
                    </Grid>
                </Grid>
                <Grid xs={12} md={12}>
                    <div className="rate-revision-btn-div">
                        <Button
                            className="submit-btn"
                            value="Save & Submit"
                            handleClick={() => onSubmitClick()}
                        />
                    </div>
                </Grid>
            </div>
        </>
    )
}

export default AddClientDetails;
