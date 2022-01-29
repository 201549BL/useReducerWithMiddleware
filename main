import { useEffect, useRef, useReducer } from "react";

const useReducerWithMiddleware = (
  reducer,
  initialValue,
  middleware,
  afterware
) => {
  const [state, dispatch] = useReducer(reducer, initialValue);
  const actionRef = useRef(null);

  const dispatchWithMiddleware = (action) => {
    actionRef.current = action;

    if (middleware) middleware(action);

    dispatch(action);
  };

  useEffect(() => {
    if (!actionRef.current) return;

    afterware(actionRef.current, state);

    actionRef.current = null;
  }, [afterware, state]);

  return { state, dispatchWithMiddleware };
};

export default useReducerWithMiddleware;
