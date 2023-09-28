import React, { useEffect, useState } from "react";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import { RootState } from "../../redux/store";
import Button from "@mui/material/Button";
import { Link } from "react-router-dom";
import DeleteForeverIcon from "@mui/icons-material/DeleteForever";
import ShowContractType from "./ShowIndividualContractType";
import {
  contractTypeData,
  deleteContractTypeData,
} from "../../actions/contractType";
import { GenericTable } from "../../common/GenericTable/GenricTable";

const TABLE_HEAD: any = [
  { label: "Contact Type", key: "contractType" },
  { label: "Action", key: "action" },
];

const ShowContractTypeTable: React.FC = () => {
  console.log("TABLE_HEAD: ", TABLE_HEAD);

  const dispatch = useAppDispatch();
  let contractTypeData = useAppSelector(
    (state: RootState) => state.contractType.allContractTypeData
  );
  let contractTypeDataRow = contractTypeData;
  const [open, setOpen] = useState(false);
  const [singleContractTypeData, setSingleContractTypeData] = useState({});
  const [filteredData, setFilteredData] = useState(contractTypeData);
  console.log("filteredData", filteredData);
  const [count, setCount] = useState(true);

  useEffect(() => {
    const contactList = contractTypeData.map((contactdate: any) => {
      const contractType = contactdate?.contractType;

      return {
        ...contactdate,
        contractType,
      };
    });
    setFilteredData(contactList);

    if (count) {
      if (contractTypeData?.length !== 0) {
        setFilteredData(
          contractTypeData?.filter((cd: { contactdate: any }) =>
            cd?.contactdate?.contactName?.toLowerCase()?.includes("")
          )
        );
        setCount(false);
      }
    }
  }, [contractTypeData, count]);

  const filterResult = (event: any) => {
    setFilteredData(contractTypeDataRow);
    let value: string = event.target.value;

    if (contractTypeData?.length !== 0) {
      const data: any = contractTypeData?.filter((ele: any) =>
        ele?.contractType?.toLowerCase()?.includes(value.toLowerCase())
      );
      console.log("filteredData inside search: ", data);

      const contactList = data?.map((contactdate: any) => {
        const contractType = contactdate?.contractType;

        return {
          ...contactdate,
          contractType,
        };
      });
      setFilteredData(contactList);
      console.log("contactList: ", contactList);
    } else {
      const contactList = contractTypeData?.map((contactdate: any) => {
        const contractType = contactdate?.contractType;

        return {
          ...contactdate,
          contractType,
        };
      });
      console.log("contactList: ", contractTypeData);
      setFilteredData(contactList);
    }
  };

  const onPressAction = (rowData: any, type: any) => {
    console.log(rowData);
    console.log(type);
  };

  return (
    <>
      <div style={{ display: "flex" }}>
        <div
          style={{ borderRadius: "15px", marginBottom: "10px", width: "90%" }}
          className="py-3 px-4"
        >
          <div className="relative max-w">
            <label htmlFor="hs-table-search" className="sr-only">
              Search
            </label>

            <input
              style={{ border: "0.5px solid gray" }}
              type="text"
              name="hs-table-search"
              id="hs-table-search"
              className="ml-[-13px] mt-[5px] p-2 pl-10 block w-[35%] border-gray-200 rounded-md text-sm focus:border-blue-500 focus:ring-blue-500 dark:bg-slate-900 dark:border-gray-700 dark:text-gray-400"
              placeholder="Search for contract types"
              onChange={(event) => filterResult(event)}
            />
            <div className="absolute inset-y-0 left-0 flex items-center pointer-events-none pl-2">
              <svg
                className="h-3.5 w-3.5 text-gray-400"
                xmlns="http://www.w3.org/2000/svg"
                width="16"
                height="16"
                fill="currentColor"
                viewBox="0 0 16 16"
              >
                <path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z" />
              </svg>
            </div>
          </div>
        </div>
        <div
          style={{
            width: "30%",
            maxHeight: "100%",
            justifyContent: "center",
            alignContent: "center",
            marginTop: "10px",
            marginLeft: "150px",
          }}
        >
          <Button
            variant="contained"
            component={Link}
            to={"/add-contract-type"}
          >
            Add contract type
          </Button>
        </div>
      </div>
      <GenericTable
        showColumnLink={["fullAddress"]}
        tableHeader={TABLE_HEAD}
        onPressAction={onPressAction}
        tableData={filteredData}
        showCheckbox={false}
        showAvatar={false}
        actionType={["Edit", "Delete"]}
        loading={true}
        onPageChange={function (page: number): void {
          throw new Error("Function not implemented.");
        }}
        count={0}
      />
    </>
  );
};

export default ShowContractTypeTable;
