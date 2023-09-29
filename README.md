import React from "react";
import Grid from "@mui/material/Unstable_Grid2";
import { TextField } from "../../common/TextField/TextField";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import { RootState } from "../../redux/store";
import { setVendorInputBoxValue } from "../../actions/vendor";
import { LocationName } from "../../constants/candidateclientconstants";
import Select from "react-select";

const VendorDetails: React.FC = () => {
    const dispatch = useAppDispatch();
    const currentVendorData = useAppSelector(
        (state: RootState) => state.vendor.vendorData
    );
    const allVendorData = useAppSelector(
        (state: RootState) => state.vendor.allVendorData
    );
    let allVendorName: object[] = [];
    if (allVendorData.length !== 0) {
        allVendorData.map((a: any) => {
            a?.addressId.map((b: any) => {
                let data = {
                    label: a.vendorId.companyName,
                    value: {
                        id: a.vendorId.id,
                        companyName: a.vendorId.companyName,
                        federalId: a.vendorId.federalId,
                        contactPerson: a.vendorId.contactPerson,
                        email: b?.contactDetailId?.email,
                        contactNumber: b?.contactDetailId?.contactNumber,
                        faxNumber: b?.contactDetailId?.faxNumber,
                        signAuthority: a.vendorId.signAuthority,
                        signAuthorityDesignation: a.vendorId.signAuthorityDesignation,
                        stateOfIncorporation: a.vendorId.stateOfIncorporation,
                        line1: b.line1,
                        line2: b.line2,
                        city: b.city,
                        zipCode: b.zipCode,
                        state: b.state,
                        country: b.country,
                    },
                };
                allVendorName.push(data);
            });
        });
    }
    const locationName = LocationName;

    const onVendorValueChange = (key: any, value: any) => {
        dispatch(setVendorInputBoxValue(key, value));
    };

    function displayVendorData(value: any) {
        onVendorValueChange("id", value.id);
        onVendorValueChange("federalID", value.federalId);
        onVendorValueChange("contactPerson", value.contactPerson);
        onVendorValueChange("email", value.email);
        onVendorValueChange("contactNumber", value.contactNumber);
        onVendorValueChange("faxNumber", value.contactNumber);
        onVendorValueChange("signAuthority", value.signAuthority);
        onVendorValueChange(
            "signAuthorityDesignation",
            value.signAuthorityDesignation
        );
        onVendorValueChange("stateOfIncorporation", value.stateOfIncorporation);
        onVendorValueChange("line1", value.line1);
        onVendorValueChange("line2", value.line2);
        onVendorValueChange("city", value.city);
        onVendorValueChange("zipCode", value.zipCode);
        onVendorValueChange("state", { label: value.state, value: value.state });
        onVendorValueChange("country", value.country);
    }

    return (
        <>
            <Grid xs={12} md={12}>
                <h2 style={{ marginTop: "40px" }}>Vendor details</h2>
            </Grid>
            <div className="flex gap-5 " style={{ margin: "auto", width: "100%" }}>
                <div className="relative overflow-x-auto w-[100%] mt-10 border border-solid">
                    <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400">
                        <thead className="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                            <tr>
                                <th scope="col" className="px-6 py-3">
                                    Vendor details
                                </th>
                                <th scope="col" className="px-6 py-3">
                                    <Select
                                        options={allVendorName}
                                        value={currentVendorData?.companyName}
                                        getOptionLabel={(option) => option.label}
                                        getOptionValue={(option) => option.value}
                                        onChange={(e: any) => {
                                            displayVendorData(e.value);
                                            onVendorValueChange("companyName", e);
                                        }}
                                        isSearchable={true}
                                    />
                                </th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Vendor federal ID</td>
                                <td className="px-6 py-4">{currentVendorData?.federalID}</td>
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Name of contact person</td>
                                <td className="px-6 py-4">
                                    {currentVendorData?.contactPerson}
                                </td>
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Vendor company email</td>
                                <td className="px-6 py-4">{currentVendorData?.email}</td>
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Vendor company contact number</td>
                                <td className="px-6 py-4">
                                    {currentVendorData?.contactNumber}
                                </td>
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Vendor fax number</td>
                                <td className="px-6 py-4">{currentVendorData?.faxNumber}</td>
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Name of sign authority</td>
                                <td className="px-6 py-4">
                                    {currentVendorData?.signAuthority}
                                </td>
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Designation of sign authority</td>
                                <td className="px-6 py-4">
                                    {currentVendorData?.signAuthorityDesignation}
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
                <div className="relative overflow-x-auto w-[100%] mt-10 border border-solid">
                    <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400">
                        <thead className="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400"></thead>
                        <tbody>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Vendor state of incorporation</td>
                                <td className="px-6 py-4">
                                    {currentVendorData?.stateOfIncorporation}
                                </td>
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Line 1</td>
                                <td className="px-6 py-4">{currentVendorData?.line1}</td>
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Line 2</td>
                                <td className="px-6 py-4">{currentVendorData?.line2}</td>
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">City</td>
                                <td className="px-6 py-4">{currentVendorData?.city}</td>
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Zipcode</td>
                                <td className="px-6 py-4">{currentVendorData?.zipCode}</td>
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">State</td>
                                <td className="px-6 py-4">{currentVendorData?.state.value}</td>
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Country</td>
                                <td className="px-6 py-4">{currentVendorData?.country}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </>
    );
};

export default VendorDetails;
