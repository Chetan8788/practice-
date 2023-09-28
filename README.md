import React, { useEffect, useState } from "react";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import { RootState } from "../../redux/store";
import Button from "@mui/material/Button";
import { Link } from "react-router-dom";
import DeleteForeverIcon from "@mui/icons-material/DeleteForever";
import ShowWorkAuthorization from "./ShowIndividualWorkAuthorization";
import { deleteWorkAuthorizationData } from "../../actions/workAuthorization";
import { GenericTable } from "../../common/GenericTable/GenricTable";

const TABLE_HEAD: any = [
  { label: "WorkAuthorization", key: "workAuthorization" },
  { label: "Action", key: "action" },
];

const ShowWorkAuthorizationTable: React.FC = () => {
  console.log("TABLE_HEAD: ", TABLE_HEAD);

  const dispatch = useAppDispatch();
  let workAuthorizationData = useAppSelector(
    (state: RootState) => state.workAuthorization.allWorkAuthorizationData
  );
  let workAuthorizationDataRow = workAuthorizationData;
  const [open, setOpen] = useState(false);
  const [singleWorkAuthorizationData, setSingleWorkAuthorizationData] =
    useState({});
  const [filteredData, setFilteredData] = useState(workAuthorizationData);
  console.log("filteredData", filteredData);
  const [count, setCount] = useState(true);

  useEffect(() => {
    const workAuthorizationList = workAuthorizationData.map((workdate: any) => {
      const workAuthorization = workdate?.workAuthorization;

      return {
        ...workdate,
        workAuthorization,
      };
    });
    setFilteredData(workAuthorizationList);

    if (count) {
      if (workAuthorizationData?.length !== 0) {
        setFilteredData(
          workAuthorizationData?.filter((cd: { workdate: any }) =>
            cd?.workdate?.workAuthorizationName?.toLowerCase()?.includes("")
          )
        );
        setCount(false);
      }
    }
  }, [workAuthorizationData, count]);

  const filterResult = (event: any) => {
    setFilteredData(workAuthorizationDataRow);
    let value: string = event.target.value;

    if (workAuthorizationData?.length !== 0) {
      const data: any = workAuthorizationData?.filter((ele: any) =>
        ele?.workAuthorization?.toLowerCase()?.includes(value.toLowerCase())
      );
      console.log("filteredData inside search: ", data);

      const workAuthorizationList = data?.map((workdate: any) => {
        const workAuthorization = workdate?.workAuthorization;

        return {
          ...workdate,
          workAuthorization,
        };
      });
      setFilteredData(workAuthorizationList);
      console.log("workAuthorizationList: ", workAuthorizationList);
    } else {
      const workAuthorizationList = workAuthorizationData.map(
        (workdate: any) => {
          const workAuthorization = workdate?.workAuthorization;

          return {
            ...workdate,
            workAuthorization,
          };
        }
      );
      console.log("workAuthorizationList: ", workAuthorizationList);
      setFilteredData(workAuthorizationList);
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
              placeholder="Search for work authorizations"
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
            to={"/add-work-authorization"}
          >
            Add work authorization
          </Button>
        </div>
      </div>
      <GenericTable
        showColumnLink={["fullAddress"]}
        // onClickRow={onClickRow}
        tableHeader={TABLE_HEAD}
        onPressAction={onPressAction}
        tableData={filteredData}
        // actionType={null}
        showCheckbox={false}
        showAvatar={false}
        actionType={["Edit", "Delete"]}
        // sortValue={""}
        loading={true}
        onPageChange={function (page: number): void {
          throw new Error("Function not implemented.");
        }}
        count={0}
      />
    </>
  );
};

export default ShowWorkAuthorizationTable;
