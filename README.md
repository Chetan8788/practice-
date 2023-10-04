import React, { useState } from "react";
import Backdrop from "@mui/material/Backdrop";
import Box from "@mui/material/Box";
// import Modal from '@mui/material/Modal';
// import Button from '@mui/material/Button';
import Typography from "@mui/material/Typography";
import { useSpring, animated } from "@react-spring/web";
import CloseIcon from "@mui/icons-material/Close";
import Grid from "@mui/material/Unstable_Grid2";
import EditIcon from "@mui/icons-material/Edit";
import DoneIcon from "@mui/icons-material/Done";
import { TextField } from "../../common/TextField/TextField";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import {
  ArticlesOfIncorporationList,
  CertificateOfInsuranceList,
  CipcicaCipcicuList,
  ClientTaskOrderOrSOWList,
  ClientTaskOrderOrSOWStepList,
  ClientTaskOrderSigningList,
  DirectDepositeAgreementList,
  DocumentationStatusList,
  EVerifyList,
  EemergencyFormList,
  GoodStandingDocumentationList,
  I9FormList,
  ListADocumentsList,
  ListBDocumentsList,
  ListCDocumentsList,
  MSAList,
  SOWList,
  VaccinationStatusList,
  VoidCheckEmailList,
  W9W4List,
  WorkAuthorizeDocumentationList,
  yesNoList,
} from "../../constants/constants";
import Select from "react-select";
import { Modal } from "../../common/Modal/Modal";
import { DropDown } from "../../common/DropDown/DropDown";
import { DatePicker } from "../../common/DatePicker/DatePicker";
import moment from "moment";
import { Button } from "../../common/Button/Button";
import { editRaterevisionData } from "../../actions/raterevision";
import { RootState } from "../../redux/store";
import { FloatLabel } from "../../common/FloatLabel/FloatLabel";

interface FadeProps {
  children: React.ReactElement;
  in?: boolean;
  onClick?: any;
  onEnter?: (node: HTMLElement, isAppearing: boolean) => void;
  onExited?: (node: HTMLElement, isAppearing: boolean) => void;
  ownerState?: any;
}

const Fade = React.forwardRef<HTMLDivElement, FadeProps>(function Fade(
  props,
  ref
) {
  const {
    children,
    in: open,
    onClick,
    onEnter,
    onExited,
    ownerState,
    ...other
  } = props;
  const style = useSpring({
    from: { opacity: 0 },
    to: { opacity: open ? 1 : 0 },
    onStart: () => {
      if (open && onEnter) {
        onEnter(null as any, true);
      }
    },
    onRest: () => {
      if (!open && onExited) {
        onExited(null as any, true);
      }
    },
  });

  return (
    <animated.div ref={ref} style={style} {...other}>
      {React.cloneElement(children, { onClick })}
    </animated.div>
  );
});

const style = {
  position: "absolute" as "absolute",
  top: "50%",
  left: "50%",
  transform: "translate(-50%, -50%)",
  width: 400,
  bgcolor: "background.paper",
  border: "1px #000",
  boxShadow: 24,
  p: 4,
  borderRadius: "10px",
};

interface Props {
  open: any;
  setOpen: any;
  data: any;
  showTableCount: any;
  int: any;
  setShowModal: any;
}

const ShowRateRevision: React.FC<Props> = ({
  open,
  setOpen,
  // data,
  showTableCount,
  int,
  setShowModal,
}) => {
  const dispatch = useAppDispatch();
  let data = useAppSelector(
    (state: RootState) => state?.rateRevision?.singleRateRevisionData
  );

  const [GrossBRValid, setGrossBRValid] = useState<boolean>();
  const [MSPfeeValid, setMSPfeeValid] = useState<boolean>();

  const [PayrateValid, setPayrateValid] = useState<boolean>();
  const [RefFeeValid, setRefFeeValid] = useState<boolean>();
  const [TaxOHpercentageValid, setTaxOHpercentageValid] = useState<boolean>();
  const [TaxOHValid, setTaxOHValid] = useState<boolean>();
  const [HealthbenefitsoptedValid, setHealthbenefitsoptedValid] =
    useState<boolean>();

  const [mspFeePercentageValid, setmspFeePercentageValid] = useState<boolean>();

  const [optedForHBValid, setoptedForHBValid] = useState<boolean>();
  const [marginValid, setmarginValid] = useState<boolean>();
  const [netPurchaseValid, setnetPurchaseValid] = useState<boolean>();
  const [rateRevisionReasonValid, setrateRevisionReasonValid] =
    useState<boolean>();
  const [netBillRatesValid, setnetBillRatesValid] = useState<boolean>();
  const [GrossBRError, setGrossBRError] = useState<any>();
  const [MSPfeepercentageError, setMSPfeepercentageError] = useState<any>();
  const [MSPfeeError, setMSPfeeError] = useState<any>();
  const [PayrateError, setPayrateError] = useState<any>();
  const [RefFeeError, setRefFeeError] = useState<any>();
  const [TaxOHpercentageError, setTaxOHpercentageError] = useState<any>();
  const [TaxOHError, setTaxOHError] = useState<any>();
  const [HealthbenefitsoptedError, setHealthbenefitsoptedError] =
    useState<any>();
  const [mspFeePercentageError, setmspFeePercentageError] = useState<any>();
  const [netBillRateError, setnetBillRateError] = useState<any>();
  const [optedForHBError, setoptedForHBError] = useState<any>();
  const [marginError, setmarginError] = useState<any>();
  const [netPurchaseError, setnetPurchaseError] = useState<any>();
  const [rateRevisionReasonError, setrateRevisionReasonValidError] =
    useState<any>();

  const [disable, setDisable] = React.useState(true);
  const [count, setCount] = React.useState(0);

  const [grossBr, setGrossBr] = React.useState(data?.grossBr);

  const [healthB, setHealthB] = React.useState(data?.healthB);

  const [margin, setMargin] = React.useState(data?.margin);

  const [mspFee, setMspFee] = React.useState(data?.mspFee);

  const [mspFeePercentage, setMspFeePercentage] = React.useState(
    data?.mspFeePercentage
  );

  const [netBillRate, setNetBillRate] = React.useState(data?.netBillRate);

  const [netPurchase, setNetPurchase] = React.useState(data?.netPurchase);

  const [optedForHB, setOptedForHB] = React.useState({
    value: data?.optedForHB,
    label: data?.optedForHB,
  });

  const [payRate, setPayRate] = React.useState(data?.payRate);

  const [rateRevisionReason, setRateRevisionReason] = React.useState(
    data?.rateRevisionReason
  );

  const [refFee, setRefFee] = React.useState(data?.refFee);

  const [taxOH, setTaxOH] = React.useState(data?.taxOH);

  const [taxOHPercentage, setTaxOHPercentage] = React.useState(
    data?.taxOHPercentage
  );

  React.useEffect(() => {
    setGrossBr(data?.grossBr);
    setHealthB(data?.healthB);
    setMargin(data?.margin);
    setMspFee(data?.mspFee);
    setMspFeePercentage(data?.mspFeePercentage);
    setNetBillRate(data?.netBillRate);
    setNetPurchase(data?.netPurchase);
    setOptedForHB({
      value: data?.optedForHB,
      label: data?.optedForHB,
    });
    setPayRate(data?.payRate);
    setRateRevisionReason(data?.rateRevision);
    setRefFee(data?.refFee);
    setTaxOH(data?.taxOH);
    setTaxOHPercentage(data?.taxOHPercentage);
    setCount(1);
  }, [data]);

  const updatingObject = {
    grossBr: grossBr,
    healthB: healthB,
    margin: margin,
    mspFee: mspFee,
    mspFeePercentage: mspFeePercentage,
    netBillRate: netBillRate,
    netPurchase: netPurchase,
    optedForHB: optedForHB.value,
    payRate: payRate,
    rateRevisionReason: rateRevisionReason,
    refFee: refFee,
    taxOH: taxOH,
    taxOHPercentage: taxOHPercentage,
    candidateId: data?.candidateId,
  };

  function updateCandidateRateRevision() {
    dispatch(editRaterevisionData(updatingObject));
    setShowModal(false);
  }

  return (
    <>
      <div className="pt-5 px-5">
        <Grid container spacing={2}>
          <Grid xs={6} md={6}>
            <FloatLabel
              label="*Gross BR"
              value={grossBr}
              handleChange={(event) => {
                setGrossBr(event?.target?.value);
              }}
            />
            {!GrossBRValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {GrossBRError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={6}>
            <FloatLabel
              label="*Health benefits"
              value={healthB}
              handleChange={(event) => {
                setHealthB(event?.target?.value);
              }}
            />
            {!HealthbenefitsoptedValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {HealthbenefitsoptedError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={6}>
            <FloatLabel
              label="*Margin"
              value={margin}
              handleChange={(event) => {
                setMargin(event?.target?.value);
              }}
            />
            {!marginValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {marginError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={6}>
            <FloatLabel
              label="*MSP fee"
              value={mspFee}
              handleChange={(event) => {
                setMspFee(event?.target?.value);
              }}
            />
            {!MSPfeeValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {MSPfeeError}
              </p>
            ) : null}
          </Grid>
          {/* <Grid xs={6} md={6}>
            <FloatLabel
              label="*MSP fee percentage"
              value={mspFeePercentage}
              handleChange={(event) => {
                setMspFeePercentage(event?.target?.value);
              }}
            />
            {!MSPfeepercentageValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {MSPfeepercentageError}
              </p>
            ) : null}
          </Grid> */}
          <Grid xs={6} md={6}>
            <FloatLabel
              label="*MSP fee percentage"
              value={mspFeePercentage}
              handleChange={(event) => {
                setMspFeePercentage(event?.target?.value);
              }}
            />
            {!mspFeePercentageValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {mspFeePercentageError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={6}>
            <FloatLabel
              label="*Net bill rate"
              value={netBillRate}
              handleChange={(event) => {
                setNetBillRate(event?.target?.value);
              }}
            />
            {!netBillRatesValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {netBillRateError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={6}>
            <FloatLabel
              label="*Net purchase"
              value={netPurchase}
              handleChange={(event) => {
                setNetPurchase(event?.target?.value);
              }}
            />
            {!netPurchaseValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {netPurchaseError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={6}>
            <Select
              placeholder="Opted for health benefits"
              value={optedForHB}
              options={yesNoList}
              onChange={(e: any) => setOptedForHB(e)}
            />
            {!optedForHBValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {optedForHBError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={6}>
            <FloatLabel
              label="*Pay rate"
              value={payRate}
              handleChange={(event) => {
                setPayRate(event?.target?.value);
              }}
            />
            {!PayrateValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {PayrateError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={6}>
            <FloatLabel
              label="*Rate revision reason"
              value={rateRevisionReason}
              handleChange={(event) => {
                setRateRevisionReason(event?.target?.value);
              }}
            />
            {!rateRevisionReasonValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {rateRevisionReasonError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={6}>
            <FloatLabel
              label="*Ref fee"
              value={refFee}
              handleChange={(e: any) => {
                setRefFee(e.target.value);
              }}
            />
            {!RefFeeValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {RefFeeError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={6}>
            <FloatLabel
              label="*Tax OH"
              value={taxOH}
              handleChange={(e: any) => {
                setTaxOH(e.target.value);
              }}
            />
            {!TaxOHValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {TaxOHError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={6}>
            <FloatLabel
              label="*Tax OH percentage"
              value={taxOHPercentage}
              handleChange={(e: any) => {
                setTaxOHPercentage(e.target.value);
              }}
            />
            {!TaxOHpercentageValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {TaxOHpercentageError}
              </p>
            ) : null}
          </Grid>
        </Grid>
        <div className="m-auto w-[50%]">
          <Button
            className="w-[50px] text-white"
            value="update"
            handleClick={() => {
              updateCandidateRateRevision();
            }}
          />
        </div>
      </div>
    </>
  );
};

export default ShowRateRevision;
