<div className="flex m-auto w-[100%]">
        <div className="container">
          <div className="arrow-steps clearfix">
            <div
              className={int === 1 ? "step current1" : "step current"}
              // className="step current"
              // className={clicked ? "step current1" : "step current"}
              onClick={() => {
                // navigate("/background-data")
                setInt(1);
              }}
            >
              {" "}
              <Typography variant="h3">Candidate details</Typography>
              {/* <span>
                    {" "}
                    <a href="#">Candidate details</a>
                  </span>{" "} */}
            </div>
            <div
              className={int === 2 ? "step current1" : "step current"}
              onClick={() => {
                // setClicked(!clicked);
                // navigate("/background-data")
                setInt(2);
              }}
            >
              {/* {" "}
                  <span>
                    <a href="#">Background Check Data</a>
                  </span>{" "} */}
              <Typography variant="h3">Background Check Data</Typography>
            </div>
            <div
              className={int === 3 ? "step current1" : "step current"}
              onClick={() => {
                // navigate("/document-data")
                setInt(3);
              }}
            >
              {/* {" "}
                  <span>
                    <a href="#">Documentation Data</a>
                  </span>{" "} */}
              <Typography variant="h3">Documentation Data</Typography>
            </div>
            <div
              className={int === 4 ? "step current1" : "step current"}
              onClick={() => {
                // navigate("/document-data")
                setInt(4);
              }}
            >
              {/* {" "}
                  <span>
                    <a href="#">Start End Operations Data</a>
                  </span>{" "} */}
              <Typography variant="h3">Start End Operations Data</Typography>
            </div>
            <div
              className={int === 5 ? "step current1" : "step current"}
              onClick={() => {
                // navigate("/document-data")
                setInt(5);
              }}
            >
              {/* {" "}
                  <span>
                    <a href="#">Rate Revision Data</a>
                  </span>{" "} */}
              <Typography variant="h3">Rate Revision Data</Typography>
            </div>
            <div
              className={
                int === 6
                  ? "step current1"
                  : "step current border-solid border-[1px]"
              }
              onClick={() => {
                // navigate("/document-data")
                setInt(6);
              }}
            >
              <Typography variant="h3">Other Data</Typography>
            </div>
          </div>

          {/* <div className="nav clearfix">
                <a href="#" className="prev">
                  Previous
                </a>
                <a href="#" className="next pull-right">
                  Next
                </a>
              </div> */}
        </div>
      </div>

      import { Typography } from "@material-tailwind/react";
