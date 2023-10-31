import React, { useState } from "react";
import { useSpring, animated, Any } from "@react-spring/web";
import { Grid, SelectChangeEvent, TextField } from "@mui/material";
import { TextField as TextField1 } from "../../common/TextField/TextField";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import Select from "react-select";
import {
  BGCAdjuStatusOptions,
  BGCAffidavitOptions,
  BGCInvoiceMonthOptions,
  BGCPackageOptions,
  BGCReportStatusOptions,
  BGCStatusOptions,
  PrimBGCInitiatedThruOptions,
  finalBGCReportOptions,
} from "../../constants/backgroundconstants";
import { Button, Button as Button1 } from "../../common/Button/Button";
import { TextArea } from "../../common/TextArea/TextArea";
import { editCandidateBackgroundCheckData } from "../../actions/backgroundCheck";
import { RootState } from "../../redux/store";
import { FloatLabel } from "../../common/FloatLabel/FloatLabel";
import { FloatSelect } from "../../common/FloatSelect/FloatSelect";
import { isTextValid } from "../../helpers/validate";

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
  showModal: any;
}

const ShowBackgroundCheck: React.FC<Props> = ({
  open,
  setOpen,
  // data,
  showTableCount,
  int,
  setShowModal,
  showModal,
}) => {
  const dispatch = useAppDispatch();
  let data = useAppSelector(
    (state: RootState) => state?.backgroundCheck?.singleBackgroundCheckData
  );

  const [disable, setDisable] = useState(true);
  const [caseID1, setCaseID1] = useState(data?.caseID1);
  const [BGCInitiatedOn, setBGCInitiatedOn] = useState(data?.BGCInitiatedOn);
  const [primaryBGCInitiatedThru, setPrimaryBGCInitiatedThru] = useState(
    data?.BGCInitiatedOn
  );

  const [BGCPackage1, setBGCPackage1] = useState(data?.BGCPackage1);
  const [BGCPackage2, setBGCPackage2] = useState(data?.BGCPackage2);
  const [BGCInvoiceMonth, setBGCInvoiceMonth] = useState(data?.BGCInvoiceMonth);
  const [BGCChargesPrimary, setBGCChargesPrimary] = useState(
    data?.BGCChargesPrimary
  );
  const [secondary, setSecondary] = useState(data?.secondary);
  const [caseID2, setCaseID2] = useState(data?.caseID2);
  const [secondaryBGCInitiatedOn, setSecondaryBGCInitiatedOn] = useState(
    data?.secondaryBGCInitiatedOn
  );
  const [secondaryBGCInitiatedThru, setSecondaryBGCInitiatedThru] = useState(
    data?.secondaryBGCInitiatedThru
  );
  const [secondaryBGCPackage1, setSecondaryBGCPackage1] = useState(
    data?.secondaryBGCPackage1
  );
  const [secondaryBGCPackage2, setSecondaryBGCPackage2] = useState(
    data?.secondaryBGCPackage2
  );
  const [secondaryBGCInvoiceMonth, setSecondaryBGCInvoiceMonth] = useState(
    data?.secondaryBGCInvoiceMonth
  );
  const [secondaryBGCCharges, setSecondaryBGCCharges] = useState(
    data?.secondaryBGCCharges
  );
  const [tertiary, setTertiary] = useState(data?.tertiary);
  const [caseID3, setCaseID3] = useState(data?.caseID3);
  const [tertiaryBGCInitiatedOn, setTertiaryBGCInitiatedOn] = useState(
    data?.tertiaryBGCInitiatedOn
  );
  const [tertiaryBGCInitiatedThru, setTertiaryBGCInitiatedThru] = useState(
    data?.tertiaryBGCInitiatedThru
  );
  const [tertiaryBGCPackage1, setTertiaryBGCPackage1] = useState(
    data?.tertiaryBGCPackage1
  );
  const [tertiaryBGCPackage2, setTertiaryBGCPackage2] = useState(
    data?.tertiaryBGCPackage2
  );
  const [tertiaryBGCInvoiceMonth, setTertiaryBGCInvoiceMonth] = useState(
    data?.tertiaryBGCInvoiceMonth
  );
  const [tertiaryBGCCharges, setTertiaryBGCCharges] = useState(
    data?.tertiaryBGCCharges
  );
  const [BGCStatus, setBGCStatus] = useState(data?.BGCStatus);
  const [BGCCompletedOn, setBGCCompletedOn] = useState(data?.BGCCompletedOn);
  const [BGCAffidavitStatus, setBGCAffidavitStatus] = useState(
    data?.BGCAffidavitStatus
  );
  const [BGCAffidavitOn, setBGCAffidavitOn] = useState(data?.BGCAffidavitOn);
  const [BGCReportStatus, setBGCReportStatus] = useState(data?.BGCReportStatus);
  const [BGCAdjuStatus, setBGCAdjuStatus] = useState(data?.BGCAdjuStatus);
  const [adjuSupportingDocs, setAdjuSupportingDocs] = useState(
    data?.adjuSupportingDocs
  );
  const [dateOfAdjudication, setDateOfAdjudication] = useState(
    data?.dateOfAdjudication
  );
  const [finalBGCReport, setFinalBGCReport] = useState(data?.finalBGCReport);
  const [BGCRemark, setBGCRemark] = useState(data?.BGCRemark);

  React.useEffect(() => {
    if (!showModal) {
      setShowSecondary(secondary);
      setShowTertiary(tertiary);
    }
  });

  React.useEffect(() => {
    setCaseID1(data?.caseID1);
    setBGCInitiatedOn(data?.BGCInitiatedOn);
    setPrimaryBGCInitiatedThru(data?.primaryBGCInitiatedThru);
    setBGCPackage1(data?.BGCPackage1);
    setBGCPackage2(data?.BGCPackage2);
    setBGCInvoiceMonth(data?.BGCInvoiceMonth);
    setBGCChargesPrimary(data?.BGCChargesPrimary);
    setSecondary(data?.secondary);
    setCaseID2(data?.caseID2);
    setSecondaryBGCInitiatedOn(data?.secondaryBGCInitiatedOn);
    setSecondaryBGCInitiatedThru(data?.secondaryBGCInitiatedThru);
    setSecondaryBGCPackage1(data?.secondaryBGCPackage1);
    setSecondaryBGCPackage2(data?.secondaryBGCPackage2);
    setSecondaryBGCInvoiceMonth(data?.secondaryBGCInvoiceMonth);
    setSecondaryBGCCharges(data?.secondaryBGCCharges);
    setTertiary(data?.tertiary);
    setCaseID3(data?.caseID3);
    setTertiaryBGCInitiatedOn(data?.tertiaryBGCInitiatedOn);
    setTertiaryBGCInitiatedThru(data?.tertiaryBGCInitiatedThru);
    setTertiaryBGCPackage1(data?.tertiaryBGCPackage1);
    setTertiaryBGCPackage2(data?.tertiaryBGCPackage2);
    setTertiaryBGCInvoiceMonth(data?.tertiaryBGCInvoiceMonth);
    setTertiaryBGCCharges(data?.tertiaryBGCCharges);
    setBGCStatus(data?.BGCStatus);
    setBGCCompletedOn(data?.BGCCompletedOn);
    setBGCAffidavitStatus(data?.BGCAffidavitStatus);
    setBGCAffidavitOn(data?.BGCAffidavitOn);
    setBGCReportStatus(data?.BGCReportStatus);
    setBGCAdjuStatus(data?.BGCAdjuStatus);
    setAdjuSupportingDocs(data?.adjuSupportingDocs);
    setDateOfAdjudication(data?.dateOfAdjudication);
    setFinalBGCReport(data?.finalBGCReport);
    setBGCRemark(data?.BGCRemark);
  }, [data]);

  const [caseID1Valid, setCaseID1Valid] = useState<boolean>();
  const [BGCInitiatedOnValid, setBGCInitiatedOnValid] = useState<boolean>();
  const [primaryBGCInitiatedThruValid, setPrimaryBGCInitiatedThruValid] =
    useState<boolean>();
  const [BGCPackage1Valid, setBGCPackage1Valid] = useState<boolean>();
  const [BGCPackage2Valid, setBGCPackage2Valid] = useState<boolean>();
  const [BGCInvoiceMonthValid, setBGCInvoiceMonthValid] = useState<boolean>();
  const [BGCChargesPrimaryValid, setBGCChargesPrimaryValid] =
    useState<boolean>();
  const [secondaryValid, setSecondaryValid] = useState<boolean>();
  const [caseID2Valid, setCaseID2Valid] = useState<boolean>();
  const [secondaryBGCInitiatedOnValid, setSecondaryBGCInitiatedOnValid] =
    useState<boolean>();
  const [secondaryBGCInitiatedThruValid, setSecondaryBGCInitiatedThruValid] =
    useState<boolean>();
  const [secondaryBGCPackage1Valid, setSecondaryBGCPackage1Valid] =
    useState<boolean>();
  const [secondaryBGCPackage2Valid, setSecondaryBGCPackage2Valid] =
    useState<boolean>();
  const [secondaryBGCInvoiceMonthValid, setSecondaryBGCInvoiceMonthValid] =
    useState<boolean>();
  const [secondaryBGCChargesValid, setSecondaryBGCChargesValid] =
    useState<boolean>();
  const [tertiaryValid, setTertiaryValid] = useState<boolean>();
  const [caseID3Valid, setCaseID3Valid] = useState<boolean>();
  const [tertiaryBGCInitiatedOnValid, setTertiaryBGCInitiatedOnValid] =
    useState<boolean>();
  const [tertiaryBGCInitiatedThruValid, setTertiaryBGCInitiatedThruValid] =
    useState<boolean>();
  const [tertiaryBGCPackage1Valid, setTertiaryBGCPackage1Valid] =
    useState<boolean>();
  const [tertiaryBGCPackage2Valid, setTertiaryBGCPackage2Valid] =
    useState<boolean>();
  const [tertiaryBGCInvoiceMonthValid, setTertiaryBGCInvoiceMonthValid] =
    useState<boolean>();
  const [tertiaryBGCChargesValid, setTertiaryBGCChargesValid] =
    useState<boolean>();
  const [BGCStatusValid, setBGCStatusValid] = useState<boolean>();
  const [BGCCompletedOnValid, setBGCCompletedOnValid] = useState<boolean>();
  const [BGCAffidavitStatusValid, setBGCAffidavitStatusValid] =
    useState<boolean>();
  const [BGCAffidavitOnValid, setBGCAffidavitOnValid] = useState<boolean>();
  const [BGCReportStatusValid, setBGCReportStatusValid] = useState<boolean>();
  const [BGCAdjuStatusValid, setBGCAdjuStatusValid] = useState<any>();
  const [adjuSupportingDocsValid, setAdjuSupportingDocsValid] =
    useState<boolean>();
  const [dateOfAdjudicationValid, setDateOfAdjudicationValid] =
    useState<boolean>();
  const [finalBGCReportValid, setFinalBGCReportValid] = useState<boolean>();
  const [BGCRemarkValid, setBGCRemarkValid] = useState<boolean>();
  const [candidateIdvalid, setcandidateIdvalid] = useState<boolean>();
  const [caseID1Error, setCaseID1Error] = useState<any>();
  const [BGCInitiatedOnError, setBGCInitiatedOnError] = useState<any>();
  const [primaryBGCInitiatedThruError, setPrimaryBGCInitiatedThruError] =
    useState<any>();
  const [BGCPackage1Error, setBGCPackage1Error] = useState<any>();
  const [BGCPackage2Error, setBGCPackage2Error] = useState<any>();
  const [BGCInvoiceMonthError, setBGCInvoiceMonthError] = useState<any>();
  const [BGCChargesPrimaryError, setBGCChargesPrimaryError] = useState<any>();
  const [secondaryError, setSecondaryError] = useState<any>();
  const [caseID2Error, setCaseID2Error] = useState<any>();
  const [secondaryBGCInitiatedOnError, setSecondaryBGCInitiatedOnError] =
    useState<any>();
  const [secondaryBGCInitiatedThruError, setSecondaryBGCInitiatedThruError] =
    useState<any>();
  const [secondaryBGCPackage1Error, setSecondaryBGCPackage1Error] =
    useState<any>();
  const [secondaryBGCPackage2Error, setSecondaryBGCPackage2Error] =
    useState<any>();
  const [secondaryBGCInvoiceMonthError, setSecondaryBGCInvoiceMonthError] =
    useState<any>();
  const [secondaryBGCChargesError, setSecondaryBGCChargesError] =
    useState<any>();
  const [tertiaryError, setTertiaryError] = useState<any>();
  const [caseID3Error, setCaseID3Error] = useState<any>();
  const [tertiaryBGCInitiatedOnError, setTertiaryBGCInitiatedOnError] =
    useState<any>();
  const [tertiaryBGCInitiatedThruError, setTertiaryBGCInitiatedThruError] =
    useState<any>();
  const [tertiaryBGCPackage1Error, setTertiaryBGCPackage1Error] =
    useState<any>();
  const [tertiaryBGCPackage2Error, setTertiaryBGCPackage2Error] =
    useState<any>();
  const [tertiaryBGCInvoiceMonthError, setTertiaryBGCInvoiceMonthError] =
    useState<any>();
  const [tertiaryBGCChargesError, setTertiaryBGCChargesError] = useState<any>();
  const [BGCStatusError, setBGCStatusError] = useState<any>();
  const [BGCCompletedOnError, setBGCCompletedOnError] = useState<any>();
  const [BGCAffidavitStatusError, setBGCAffidavitStatusError] = useState<any>();
  const [BGCAffidavitOnError, setBGCAffidavitOnError] = useState<any>();
  const [BGCReportStatusError, setBGCReportStatusError] = useState<any>();
  const [BGCAdjuStatusError, setBGCAdjuStatusError] = useState<any>();
  const [adjuSupportingDocsError, setAdjuSupportingDocsError] = useState<any>();
  const [dateOfAdjudicationError, setDateOfAdjudicationError] = useState<any>();
  const [finalBGCReportError, setFinalBGCReportError] = useState<any>();
  const [BGCRemarkError, setBGCRemarkError] = useState<any>();

  const [showSecondary, setShowSecondary] = useState<boolean>(false);
  const [showTertiary, setShowTertiary] = useState<boolean>(false);
  const [candidateId, setCandidateId] = useState(data?.candidateId);
  const [count, setCount] = React.useState(0);

  function updateCandidateBackground() {
    setCaseID1Valid(isTextValid(caseID1));
    setBGCInitiatedOnValid(isTextValid(BGCInitiatedOn));
    setPrimaryBGCInitiatedThruValid(isTextValid(primaryBGCInitiatedThru));
    setBGCPackage1Valid(isTextValid(BGCPackage1));
    setBGCPackage2Valid(isTextValid(BGCPackage2));
    setBGCInvoiceMonthValid(isTextValid(BGCInvoiceMonth));
    setBGCChargesPrimaryValid(isTextValid(BGCChargesPrimary));
    setCaseID2Valid(isTextValid(caseID2));
    setSecondaryBGCInitiatedOnValid(isTextValid(secondaryBGCInitiatedOn));
    setSecondaryBGCInitiatedThruValid(isTextValid(secondaryBGCInitiatedThru));
    setSecondaryBGCPackage1Valid(isTextValid(secondaryBGCPackage1));
    setSecondaryBGCPackage2Valid(isTextValid(secondaryBGCPackage2));
    setSecondaryBGCInvoiceMonthValid(isTextValid(secondaryBGCInvoiceMonth));
    setSecondaryBGCChargesValid(isTextValid(secondaryBGCCharges));
    setTertiaryValid(isTextValid(tertiary));
    setCaseID3Valid(isTextValid(caseID3));
    setTertiaryBGCInitiatedOnValid(isTextValid(tertiaryBGCInitiatedOn));
    setTertiaryBGCInitiatedThruValid(isTextValid(tertiaryBGCInitiatedThru));
    setTertiaryBGCPackage1Valid(isTextValid(tertiaryBGCPackage1));
    setTertiaryBGCPackage2Valid(isTextValid(tertiaryBGCPackage2));
    setTertiaryBGCInvoiceMonthValid(isTextValid(tertiaryBGCInvoiceMonth));
    setTertiaryBGCChargesValid(isTextValid(tertiaryBGCCharges));
    setBGCStatusValid(isTextValid(BGCStatus));
    setBGCCompletedOnValid(isTextValid(BGCCompletedOn));
    setBGCAffidavitStatusValid(isTextValid(BGCAffidavitStatus));

    setBGCAffidavitOnValid(isTextValid(BGCAffidavitOn));
    setBGCReportStatusValid(isTextValid(BGCReportStatus));
    setBGCAdjuStatusValid(isTextValid(BGCAdjuStatus));
    setAdjuSupportingDocsValid(isTextValid(adjuSupportingDocs));
    setDateOfAdjudicationValid(isTextValid(dateOfAdjudication));
    setFinalBGCReportValid(isTextValid(finalBGCReport));
    setBGCStatusValid(isTextValid(BGCStatus));
    setBGCRemarkValid(isTextValid(BGCRemark));

    if (
      primaryBGCInitiatedThruValid &&
      caseID1Valid &&
      BGCInitiatedOnValid &&
      BGCPackage1Valid &&
      // BGCPackage1 &&
      BGCPackage2Valid &&
      BGCInvoiceMonthValid &&
      BGCChargesPrimaryValid &&
      secondaryValid &&
      caseID2Valid &&
      secondaryBGCInitiatedOnValid &&
      secondaryBGCInitiatedThruValid &&
      secondaryBGCPackage1Valid &&
      secondaryBGCPackage2Valid &&
      secondaryBGCInvoiceMonthValid &&
      secondaryBGCChargesValid &&
      tertiaryValid &&
      caseID3Valid &&
      tertiaryBGCInitiatedOnValid &&
      tertiaryBGCInitiatedThruValid &&
      tertiaryBGCPackage1Valid &&
      tertiaryBGCPackage2Valid &&
      tertiaryBGCInvoiceMonthValid &&
      tertiaryBGCChargesValid &&
      BGCStatusValid &&
      BGCCompletedOnValid &&
      BGCAffidavitStatusValid &&
      BGCAffidavitOnValid &&
      BGCReportStatusValid &&
      BGCAdjuStatusValid &&
      adjuSupportingDocsValid &&
      dateOfAdjudicationValid &&
      finalBGCReportValid &&
      BGCRemarkValid &&
      candidateIdvalid
    ) {
      dispatch(
        editCandidateBackgroundCheckData(
          caseID1,
          BGCInitiatedOn,
          primaryBGCInitiatedThru,
          BGCPackage1,
          BGCPackage2,
          BGCInvoiceMonth,
          BGCChargesPrimary,
          secondary,
          caseID2,
          secondaryBGCInitiatedOn,
          secondaryBGCInitiatedThru,
          secondaryBGCPackage1,
          secondaryBGCPackage2,
          secondaryBGCInvoiceMonth,
          secondaryBGCCharges,
          tertiary,
          caseID3,
          tertiaryBGCInitiatedOn,
          tertiaryBGCInitiatedThru,
          tertiaryBGCPackage1,
          tertiaryBGCPackage2,
          tertiaryBGCInvoiceMonth,
          tertiaryBGCCharges,
          BGCStatus,
          BGCCompletedOn,
          BGCAffidavitStatus,
          BGCAffidavitOn,
          BGCReportStatus,
          BGCAdjuStatus,
          adjuSupportingDocs,
          dateOfAdjudication,
          finalBGCReport,
          BGCRemark,
          data?.candidateId
        )
      );

      setShowModal(false);
    } else {
      if (!caseID1Valid) {
        setCaseID1Error("caseID1 should not be empty.");
      }
      if (!BGCInitiatedOnValid) {
        setBGCInitiatedOnError(" BGCInitiatedOn should not be empty.");
      }
      if (!primaryBGCInitiatedThruValid) {
        setPrimaryBGCInitiatedThruError(
          "primaryBGCInitiatedThru should not be empty."
        );
      }
      if (!BGCPackage1Valid) {
        setBGCPackage1Error("BGCPackage1 should not be empty.");
      }
      if (!BGCPackage2Valid) {
        setBGCPackage2Error("BGCPackage2 date should not be empty.");
      }
      if (!BGCInvoiceMonthValid) {
        setBGCInvoiceMonthError("BGCInvoiceMonth should not be empty.");
      }
      if (!BGCChargesPrimaryValid) {
        setBGCChargesPrimaryError("BGCChargesPrimary should not be empty.");
      }
      if (!secondaryValid) {
        setSecondaryError("secondary should not be empty.");
      }
      if (!caseID2Valid) {
        setCaseID2Error("caseID2 should not be empty.");
      }
      if (!secondaryBGCInitiatedOnValid) {
        setSecondaryBGCInitiatedOnError(
          "secondaryBGCInitiatedOn should not be empty."
        );
      }
      if (!secondaryBGCInitiatedThruValid) {
        setSecondaryBGCInitiatedThruError(
          "secondaryBGCInitiatedThru should not be empty."
        );
      }
      if (!secondaryBGCPackage1Valid) {
        setSecondaryBGCPackage1Error(
          "secondaryBGCPackage1 should not be empty"
        );
      }
      if (!secondaryBGCPackage2Valid) {
        setSecondaryBGCPackage2Error(
          "secondaryBGCPackage2 should not be empty."
        );
      }
      if (!secondaryBGCInvoiceMonthValid) {
        setSecondaryBGCInvoiceMonthError(
          "secondaryBGCInvoiceMonth should not be empty."
        );
      }
      if (!secondaryBGCChargesValid) {
        setSecondaryBGCChargesError("secondaryBGCCharges should not be empty.");
      }
      if (!tertiaryValid) {
        setTertiaryError("tertiary should not be empty.");

        if (!caseID3Valid) {
          setCaseID3Error("caseID3 should not be empty.");
        }
        if (!tertiaryBGCInitiatedOnValid) {
          setTertiaryBGCInitiatedOnError(
            "tertiaryBGCInitiatedOn should not be empty."
          );
        }
        if (!tertiaryBGCInitiatedThruValid) {
          setTertiaryBGCInitiatedThruError(
            "tertiaryBGCInitiatedThru should not be empty."
          );
        }
        if (!tertiaryBGCPackage1Valid) {
          setTertiaryBGCPackage1Error(
            "tertiaryBGCPackage1 should not be empty."
          );
        }
        if (!tertiaryBGCPackage2Valid) {
          setTertiaryBGCPackage2Error(
            "tertiaryBGCPackage2 should not be empty."
          );
        }
        if (!tertiaryBGCInvoiceMonthValid) {
          setTertiaryBGCInvoiceMonthError(
            "tertiaryBGCInvoiceMonth should not be empty."
          );
        }
        if (!tertiaryBGCChargesValid) {
          setTertiaryBGCChargesError("tertiaryBGCCharges should not be empty.");
        }
        if (!BGCStatusValid) {
          setBGCStatusError("BGCStatus should not be empty.");
        }
        if (!BGCCompletedOnValid) {
          setBGCCompletedOnError("BGCCompletedOn should not be empty.");
        }
        if (!BGCAffidavitStatusValid) {
          setBGCAffidavitStatusError("BGCAffidavitStatus should not be empty.");
        }

        if (!BGCAffidavitOnValid) {
          setBGCAffidavitOnError("BGCAffidavitOn should not be empty.");

          if (!BGCReportStatusValid) {
            setBGCReportStatusError("BGCReportStatus should not be empty.");
          }
          if (!BGCAdjuStatusValid) {
            setBGCAdjuStatusError("BGCAdjuStatus should not be empty.");
          }
          if (!adjuSupportingDocsValid) {
            setAdjuSupportingDocsError(
              "adjuSupportingDocs should not be empty."
            );
          }
          if (!dateOfAdjudicationValid) {
            setDateOfAdjudicationError(
              "dateOfAdjudication should not be empty."
            );
          }
          if (!finalBGCReportValid) {
            setFinalBGCReportError("finalBGCReport should not be empty.");
          }
          if (!BGCRemarkValid) {
            setBGCRemarkError("BGCRemark should not be empty.");
          }
        }
      }
    }
  }

  return (
    <>
      <div className="pt-10 pl-10 h-[70vh] overflow-auto" id="no-scroll-div">
        <Grid container spacing={2} columnGap={"15px"}>
          <Grid xs={6} md={5.5}>
            <FloatLabel
              label="CaseID1"
              value={caseID1}
              placeholder={""}
              handleChange={(e: any) => {
                setCaseID1(e.target.value);
                setCaseID1Valid(isTextValid(e.target.value));
              }}
            />
            {!caseID1Valid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {caseID1Error}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatLabel
              label="BGC initiated On"
              // label="BGC Initiated On"
              value={BGCInitiatedOn}
              type="date"
              placeholder={""}
              handleChange={(e) => {
                setBGCInitiatedOn(e.target.value);
                setBGCInitiatedOnValid(isTextValid(e.target.value));
              }}
            />
            {!BGCInitiatedOnValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {BGCInitiatedOnError}
              </p>
            ) : null}
          </Grid>

          <Grid xs={6} md={5.5}>
            <FloatSelect
              labelId={"Primary BGC initiated thru"}
              label="Primary BGC initiated thru"
              options={PrimBGCInitiatedThruOptions}
              value={primaryBGCInitiatedThru}
              handleChange={(e: any) => {
                setPrimaryBGCInitiatedThruValid(isTextValid(e.target.value));
                setPrimaryBGCInitiatedThru(e.target.value);
              }}
              styles={{
                border: "none",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!primaryBGCInitiatedThruValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {primaryBGCInitiatedThruError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatSelect
              labelId={"BGC package 1"}
              label="BGC package 1"
              options={BGCPackageOptions}
              value={BGCPackage1}
              handleChange={(e: any) => {
                setBGCPackage1Valid(isTextValid(e.target.value));
                setBGCPackage1(e.target.value);
              }}
              styles={{
                border: "none",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!BGCPackage1Valid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {BGCPackage1Error}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatSelect
              label="BGC package 2"
              labelId={"BGC package 2"}
              options={BGCPackageOptions}
              value={BGCPackage2}
              handleChange={(e: any) => {
                setBGCPackage2Valid(isTextValid(e.target.value));
                setBGCPackage2(e.target.value);
              }}
              styles={{
                border: "none",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!BGCPackage2Valid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {BGCPackage2Error}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatSelect
              label="BGC invoice month"
              labelId={"BGC invoice month"}
              options={BGCInvoiceMonthOptions}
              value={BGCInvoiceMonth}
              handleChange={(e: any) => {
                setBGCInvoiceMonth(e.target.value);
                setBGCInvoiceMonthValid(isTextValid(e.target.value));
              }}
              styles={{
                border: "none",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!BGCInvoiceMonthValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {BGCInvoiceMonthError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatLabel
              label={"BGC charges primary"}
              value={BGCChargesPrimary}
              handleChange={(e: any) => {
                setBGCChargesPrimary(e.target.value);
                setBGCChargesPrimaryValid(isTextValid(e.target.value));
              }}
              placeholder={""}
              styles={{
                border: "1px solid hsl(0, 0%, 80%)",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!BGCChargesPrimaryValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {BGCChargesPrimaryError}
              </p>
            ) : null}
          </Grid>
          {/* {!showSecondary ? (
            <div className="add-cancel-1">
              <Button1
                className="btn-size"
                value="+"
                handleClick={() => {
                  // dispatch(setSecondaryButton(true));
                  setShowSecondary(true);
                  setSecondary(true);
                }}
              />
            </div>
          ) : null} */}
          <Grid xs={6} md={5.5}>
            <FloatLabel
              label="case ID-2"
              value={caseID2}
              placeholder={""}
              handleChange={(e: any) => {
                setCaseID2(e.target.value);
                setCaseID2Valid(isTextValid(e.target.value));
              }}
              className=""
            />
            {!caseID2Valid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {caseID2Error}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatLabel
              label="Secondary BGC Initiated On"
              value={secondaryBGCInitiatedOn}
              type="date"
              placeholder={""}
              handleChange={(e) => {
                setSecondaryBGCInitiatedOn(e.target.value);
                setSecondaryBGCInitiatedOnValid(isTextValid(e.target.value));
              }}
            />
            {!secondaryBGCInitiatedOnValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {secondaryBGCInitiatedOnError}
              </p>
            ) : null}
          </Grid>

          <Grid xs={6} md={5.5}>
            <FloatSelect
              labelId={"Secondary BGC initiated thru"}
              label="Secondary BGC initiated thru"
              options={PrimBGCInitiatedThruOptions}
              value={secondaryBGCInitiatedThru}
              handleChange={(e: any) => {
                setSecondaryBGCInitiatedThru(e.target.value);
                setSecondaryBGCInitiatedThruValid(isTextValid(e.target.value));
              }}
              styles={{
                border: "none",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!secondaryBGCInitiatedThruValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {secondaryBGCInitiatedThruError}
              </p>
            ) : null}
          </Grid>

          <Grid xs={6} md={5.5}>
            <FloatSelect
              labelId={"Secondary BGC check-1"}
              label="Secondary BGC check-1"
              options={BGCPackageOptions}
              value={secondaryBGCPackage1}
              handleChange={(e: any) => {
                setSecondaryBGCPackage1(e.target.value);
                setSecondaryBGCPackage1Valid(isTextValid(e.target.value));
              }}
              styles={{
                border: "none",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!secondaryBGCPackage1Valid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {secondaryBGCPackage1Error}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatSelect
              labelId={"Secondary BGC check-2"}
              label="Secondary BGC check-2"
              options={BGCPackageOptions}
              value={secondaryBGCPackage2}
              handleChange={(e: any) => {
                setSecondaryBGCPackage2(e.target.value);
                setSecondaryBGCPackage2Valid(isTextValid(e.target.value));
              }}
              styles={{
                border: "none",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!secondaryBGCPackage2Valid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {secondaryBGCPackage2Error}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatSelect
              labelId={"Secondary BGC invoice month"}
              label="Secondary BGC invoice month"
              options={BGCInvoiceMonthOptions}
              value={secondaryBGCInvoiceMonth}
              handleChange={(e: any) => {
                setSecondaryBGCInvoiceMonth(e.target.value);
                setSecondaryBGCInvoiceMonthValid(isTextValid(e.target.value));
              }}
              // handleChange={(e: any) => setSecondaryBGCInvoiceMonth(e)}
              styles={{
                border: "none",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!secondaryBGCInvoiceMonthValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {secondaryBGCInvoiceMonthError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatLabel
              label={"BGC charges Secondary"}
              value={secondaryBGCCharges}
              handleChange={(e) => {
                setSecondaryBGCCharges(e.target.value);
                setSecondaryBGCChargesValid(isTextValid(e.target.value));
              }}
              placeholder={""}
              styles={{
                border: "1px solid hsl(0, 0%, 80%)",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!secondaryBGCChargesValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {secondaryBGCChargesError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatLabel
              label="case ID-3"
              value={caseID3}
              placeholder={""}
              handleChange={(e) => {
                setCaseID3(e.target.value);
                setCaseID3Valid(isTextValid(e.target.value));
              }}
            />
            {!caseID3Valid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {caseID3Error}
              </p>
            ) : null}
          </Grid>

          <Grid xs={6} md={5.5}>
            <FloatLabel
              label="Tertiary BGC initiated on"
              value={tertiaryBGCInitiatedOn}
              type="date"
              placeholder={""}
              handleChange={(e) => {
                setTertiaryBGCInitiatedOn(e.target.value);
                setTertiaryBGCInitiatedOnValid(isTextValid(e.target.value));
              }}
            />
            {!tertiaryBGCInitiatedOnValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {tertiaryBGCInitiatedOnError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatSelect
              labelId={"Tertiary BGC initiated thru"}
              label="Tertiary BGC initiated thru"
              options={PrimBGCInitiatedThruOptions}
              value={tertiaryBGCInitiatedThru}
              handleChange={(e: any) => {
                setTertiaryBGCInitiatedThru(e.target.value);
                setTertiaryBGCInitiatedThruValid(isTextValid(e.target.value));
              }}
              styles={{
                border: "none",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!tertiaryBGCInitiatedThruValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {tertiaryBGCInitiatedThruError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatSelect
              labelId={"Tertiary BGC check-1"}
              label="Tertiary BGC check-1"
              options={BGCPackageOptions}
              value={tertiaryBGCPackage1}
              handleChange={(e: any) => {
                setTertiaryBGCPackage1(e.target.value);
                setTertiaryBGCPackage1Valid(isTextValid(e.target.value));
              }}
              styles={{
                border: "none",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!tertiaryBGCPackage1Valid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {tertiaryBGCPackage1Error}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatSelect
              labelId={"Tertiary BGC check-2"}
              label="Tertiary BGC check-2"
              options={BGCPackageOptions}
              value={tertiaryBGCPackage2}
              handleChange={(e: any) => {
                setTertiaryBGCPackage2(e.target.value);
                setTertiaryBGCPackage2Valid(isTextValid(e.target.value));
              }}
              styles={{
                border: "none",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!tertiaryBGCPackage2Valid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {tertiaryBGCPackage2Error}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatSelect
              labelId={"Tertiary BGC invoice month"}
              label="Tertiary BGC invoice month"
              options={BGCInvoiceMonthOptions}
              value={tertiaryBGCInvoiceMonth}
              handleChange={(e: any) => {
                setTertiaryBGCInvoiceMonth(e.target.value);
                setTertiaryBGCInvoiceMonthValid(isTextValid(e.target.value));
              }}
              styles={{
                border: "none",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!tertiaryBGCInvoiceMonthValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {tertiaryBGCInvoiceMonthError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatLabel
              label="BGC charges Tertiary"
              value={tertiaryBGCCharges}
              handleChange={(e) => {
                setTertiaryBGCCharges(e.target.value);
                setTertiaryBGCChargesValid(isTextValid(e.target.value));
              }}
              placeholder={""}
            />
            {!tertiaryBGCChargesValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {tertiaryBGCChargesError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatSelect
              labelId={"BGC Status Options"}
              label="BGC Status Options"
              options={BGCStatusOptions}
              value={BGCStatus}
              handleChange={(e: any) => {
                setBGCStatus(e.target.value);
                setBGCStatusValid(isTextValid(e.target.value));
              }}
              styles={{
                border: "none",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!BGCStatusValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {BGCStatusError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatLabel
              label="BGC completed on"
              value={BGCCompletedOn}
              type="date"
              handleChange={(e) => {
                setBGCCompletedOn(e.target.value);
                setBGCCompletedOnValid(isTextValid(e.target.value));
              }}
              placeholder={""}
            />
            {!BGCCompletedOnValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {BGCCompletedOnError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatSelect
              labelId={"BGC affidavit status"}
              label="BGC affidavit status"
              options={BGCAffidavitOptions}
              value={BGCAffidavitStatus}
              handleChange={(e: any) => {
                setBGCAffidavitStatus(e.target.value);
                setBGCAffidavitStatusValid(isTextValid(e.target.value));
              }}
              styles={{
                border: "none",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!BGCAffidavitStatusValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {BGCAffidavitStatusError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatSelect
              labelId={"BGC adjudication Status"}
              label="BGC adjudication Status"
              options={BGCAdjuStatusOptions}
              value={BGCAdjuStatus}
              handleChange={(e: any) => {
                setBGCAdjuStatus(e.target.value);
                setBGCAdjuStatusValid(isTextValid(e.target.value));
              }}
              styles={{
                border: "none",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!BGCAdjuStatusValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {BGCAdjuStatusError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatLabel
              label="Adjudication supporting document"
              value={adjuSupportingDocs}
              handleChange={(e) => {
                setAdjuSupportingDocs(e.target.value);
                setAdjuSupportingDocsValid(isTextValid(e.target.value));
              }}
              placeholder={""}
            />
            {!adjuSupportingDocsValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {adjuSupportingDocsError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatLabel
              label="Date of adjudication"
              value={dateOfAdjudication}
              type="date"
              handleChange={(e) => {
                setDateOfAdjudication(e.target.value);
                setDateOfAdjudicationValid(isTextValid(e.target.value));
              }}
              placeholder={""}
            />
            {!dateOfAdjudicationValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {dateOfAdjudicationError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatSelect
              labelId={"Final BGC report status"}
              label="Final BGC report status"
              options={finalBGCReportOptions}
              value={finalBGCReport}
              handleChange={(e: any) => {
                setFinalBGCReport(e.target.value);
                setFinalBGCReportValid(isTextValid(e.target.value));
              }}
              styles={{
                border: "none",
                textAlign: "left",
                width: "100%",
                height: "38px",
                borderRadius: "none",
                fontSize: "14px",
              }}
            />
            {!finalBGCReportValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {finalBGCReportError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.5}>
            <FloatLabel
              label="BGC remark"
              value={BGCRemark}
              placeholder={""}
              handleChange={(e) => {
                setBGCRemark(e.target.value);
                setBGCRemarkValid(isTextValid(e.target.value));
              }}
            />
            {!BGCRemarkValid ? (
              <p
                className=""
                style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
              >
                {BGCRemarkError}
              </p>
            ) : null}
          </Grid>
        </Grid>
        <div className="m-auto w-[20%] ml-[35%] text-white ">
          <Button
            className=""
            value="Update"
            handleClick={() => {
              updateCandidateBackground();
            }}
            styles={{ fontSize: "16px" }}
          />
        </div>
      </div>
    </>
  );
};

export default ShowBackgroundCheck;

